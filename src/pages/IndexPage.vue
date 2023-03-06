<template>
  <q-page class="row items-center justify-evenly">
    <FormComponent />
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import FormComponent from 'src/components/FormComponent.vue';

export default defineComponent({
  components: {
    FormComponent,
  },

});

</script>
