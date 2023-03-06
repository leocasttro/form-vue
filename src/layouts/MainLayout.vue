<template>
  <q-layout>
    <q-header class="bg-secondary">
      <div class="row justify-between">
        <div class="col-xs-4 col-sm-5 col-md-5">
        <q-img class="q-ml-md"
          src="../assets/icon.png"
          loading="lazy"
          spinner-color="white"
          height="90px"
          style="max-width: 100px"
        />
        </div>
        <div class="col-xs-4 col-sm-5 col-md-5">
          <h1>Denúncia</h1>
        </div>
        <div class="login column">
          <span class="material-icons">
            account_circle
          </span>
        </div>
      </div>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MainLayout',

});
</script>

<style scoped>
h1 {
  font-weight: 400;
  font-size: 30px;
  margin: 0;
}
.login {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 40px;
  margin: 0px 40px;
}
.login p {
  font-size: 15px;
}
</style>
