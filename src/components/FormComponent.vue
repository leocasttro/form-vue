<template>
<div class="q-pa-xl" style="width: 700px;">
  <q-form
    @submit="submitForm"
    class="q-gutter-md">
    <q-input
      square outlined
      v-model="form.companyName"
      label="Nome da empresa"
    />
    <div class="map">
      <q-input
        square outlined
        v-model="form.address"
        @click="showMap"
        @change="geocodeAddress(form.address)"
        label="Endereço"
      />
      <MapComponent v-if="map"/>
    </div>
    <q-input
      square outlined
      v-model="form.name"
      label="Nome do consumidor"
    />
    <q-input
      square outlined
      v-model="form.email"
      label="E-mail"
    />
    <q-input
      square outlined
      v-model="form.phone"
      label="Telefone"
      mask="(##) #####-####"
    />
    <q-file borderless bottom-slots v-model="form.imageFile" label="imagens" counter>
      <template v-slot:prepend>
        <q-icon name="cloud_upload" @click.stop.prevent />
      </template>
      <template v-slot:append>
        <q-icon name="close" @click.stop.prevent="form.imageFile = null" class="cursor-pointer" />
      </template>
    </q-file>

    <q-input
      square outlined
      type="textarea"
      v-model="form.description"
      label="Descrição da denúncia (Max 1024 caracteres)"
    />

    <div>
      <q-btn label="Enviar" type="submit" color="secondary"
      style="width: 100%;"/>
    </div>
  </q-form>

</div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';
import { Form } from './models';
import MapComponent from './MapComponent.vue';

export default defineComponent({
  components: {
    MapComponent,
  },
  data() {
    const map = false;
    const form = reactive<Form>({
      companyName: '',
      address: '',
      name: '',
      email: '',
      phone: '',
      imageFile: null,
      description: '',
    });
    return { form, map };
  },
  methods: {
    submitForm() {
      this.$q.notify({
        message: 'Reclamação cadastrada',
        color: 'green-6',
        icon: 'check_circle_outline',
      });
      this.resetForm();
    },

    resetForm() {
      this.form = reactive<Form>({
        companyName: '',
        address: '',
        name: '',
        email: '',
        phone: '',
        imageFile: null,
        description: '',
      });
    },

    async geocodeAddress(address: string): Promise<{ lat: number, lng: number }> {
      const encodeAddres = encodeURIComponent(address);
      const url = `https://nominatim.openstreetmap.org/search?q=${encodeAddres}&format=json`;

      const response = await fetch(url);
      const data = await response.json();

      if (data.length === 0) {
        throw new Error('Não foi possível obter as coordenadas para o endereço');
      }

      const location = data[0];
      return { lat: parseFloat(location.lat), lng: parseFloat(location.lon) };
    },

    showMap() {
      this.map = true;
    },
  },
});
</script>

<style scoped>
q-input {
  width: 90%;
}
</style>
