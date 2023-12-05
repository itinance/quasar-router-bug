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
