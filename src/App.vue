<script setup>
import homeView from './views/homeView.vue';
import { RouterView } from 'vue-router';
</script>

<template>
<h1 class="titulo">livraria</h1>
  <div class="container-geral">
    <RouterView/>
  </div>
</template>

<style scoped>

.container-geral {
  /* display: flex;
  justify-content: space-between; */
  display: grid;
  grid-template-columns: 3fr 1fr;
  
}

</style>