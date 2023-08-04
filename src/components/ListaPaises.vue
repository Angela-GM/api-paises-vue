<script setup lang="ts">
import { onMounted, ref } from 'vue';

const data = ref([]);


onMounted(async () => {
  try {
    const response = await fetch('https://restcountries.com/v3.1/all');
    data.value = await response.json();
    console.log(data);
    
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}); 



</script>


<template>
    <div>
        <h1>Lista de Paises</h1>
        <ul>
        <li v-for="pais in data" :key="pais.name.common">
            {{ pais.name.common }}
        </li>
        </ul>
    </div>

    
 
    
</template>




<style scoped></style>