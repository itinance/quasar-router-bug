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
          <q-btn align="left" class="btn-fixed-width" color="primary" label="Go to test page using Router" @click="doRedirect"/>
        </div>
      </div>

      <div class="row">
        <div>
          <br><br>
          Ugly workaround using plain vanilla javascript:

          <q-btn align="left" class="btn-fixed-width" color="orange" label="Workaround: Go to test page with window.location" @click="doWorkaround"/>
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

    const doWorkaround = () => {
      console.log('doWorkaround');
      window.location.href = '/test';
    }

    return {doRedirect, doWorkaround};
  }
});
</script>
