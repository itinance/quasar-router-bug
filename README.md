# Router Test (routertest)

A test to investigate router related issues.

Given is a **VueJS 3** application, based on Quasar and I am struggling to use the **Router** programmatically.

The issue is described best like this:

# 1. The Problem

When I push the User to another route, only the URL in the browser will be updated, but the corresponding Component will not get rendered.
I have to manually refresh the web page in the Webbrowser in order to get the corresponding component rendered properly.

# 2. What happens instead?

3.1 This is the index page, containing the button that shall send the user to another page:

[![enter image description here][1]][1]

3.2. When I click on the Button, the URL will be updated correctly but the test-component won't get rendered at all:

[![enter image description here][2]][2]

3.3. But when I refresh the web browser now manually (or navigate to that particular URL), it will render the test component:

[![enter image description here][3]][3]



# 3. Code

I have published a full working example on GitHub: https://github.com/itinance/quasar-router-bug

The router is configured in history-mode, but this doesn't matter as the issue appears also in the hash-mode.

Here are my routes:

    import { RouteRecordRaw } from 'vue-router';

    const routes: RouteRecordRaw[] = [
      {
        path: '/',
        component: () => import('layouts/MainLayout.vue'),
        children: [{ path: '', component: () => import('pages/IndexPage.vue') }],
      },

      {
        path: '/test',
        name: 'test',
        component: () => import('layouts/MainLayout.vue'),
        children: [{ path: '', component: () => import('pages/TestPage.vue') }],
      },

      // Always leave this as last one,
      // but you can also remove it
      {
        path: '/:catchAll(.*)*',
        component: () => import('pages/ErrorNotFound.vue'),
      },
    ];

    export default routes;

Here is my Index-Component, that contains a button where I want to send the user programmatically to another page:

    <template>
      <q-page class="row items-center justify-evenly">

        <div class="q-pa-md example-row-equal-width">
          <div class="row">
            <div>INDEX PAGE</div>
          </div>


          <div class="row">
            <div>
              In order to navigate to the test page, you need to manually reload the page after clicking the button.
              Otherwise, only a white page will be rendered.

              <q-btn align="left" class="btn-fixed-width" color="primary" label="Go to test page" @click="doRedirect"/>
            </div>
          </div>


        </div>
      </q-page>
    </template>

    <script lang="ts">
    import {Todo, Meta} from 'components/models';
    import ExampleComponent from 'components/ExampleComponent.vue';
    import {defineComponent, ref} from 'vue';
    import {dom} from 'quasar';
    import {useRouter} from 'vue-router';

    export default defineComponent({
      name: 'IndexPage',
      computed: {
        dom() {
          return dom
        }
      },
      components: {},
      setup() {

        const router = useRouter();

        const doRedirect = () => {
          console.log('doRedirect');
          router.push({name: 'test'});
        }
        return {doRedirect};
      }
    });
    </script>

And this is the test-component, which is the target component where I want to use send:

    <template>
      <q-page class="row items-center justify-evenly">

        <div class="q-pa-md example-row-equal-width">
          <div>
            TEST PAGE

            this will only be rendered after manual page-reload

          </div>
        </div>
      </q-page>
    </template>

    <script lang="ts">
    import { Todo, Meta } from 'components/models';
    import ExampleComponent from 'components/ExampleComponent.vue';
    import { defineComponent, ref } from 'vue';

    export default defineComponent({
      name: 'TestPage',
      setup () {
        return { };
      }
    });
    </script>


[1]: https://i.stack.imgur.com/Z4mBw.png
[2]: https://i.stack.imgur.com/DkcXb.png
[3]: https://i.stack.imgur.com/XKzLu.png


## Install the dependencies
```bash
yarn
# or
npm install
```

### Start the app in development mode (hot-code reloading, error reporting, etc.)
```bash
quasar dev
```


### Lint the files
```bash
yarn lint
# or
npm run lint
```


### Format the files
```bash
yarn format
# or
npm run format
```



### Build the app for production
```bash
quasar build
```

### Customize the configuration
See [Configuring quasar.config.js](https://v2.quasar.dev/quasar-cli-vite/quasar-config-js).
