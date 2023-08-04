<template>
    <h1>Listado de Paises</h1>
    
</template>

<script setup lang="ts">
import { onMounted } from 'vue';

onMounted(async () => {
  try {
    const response = await fetch('https://restcountries.com/v3.1/all');
    const data = await response.json();
    console.log(data);
    
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});


    



</script>


<style scoped></style>