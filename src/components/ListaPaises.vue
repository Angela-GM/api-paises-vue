<script setup lang="ts">
import { onMounted, ref } from 'vue';

interface Country {
  name: {
    common: string;
  };
  flags: {
    png: string;
    alt: string;
  };
  cca2: string; 
}

const data = ref<Country[]>([]);
const neighboringCountries = ref<Country[]>([]);
const apiKey = import.meta.env.VITE_APP_KEY;

onMounted(async () => {
  try {
    const response = await fetch('https://restcountries.com/v3.1/all');
    const countries: Country[] = await response.json();
    data.value = countries;
    console.log(data.value[5].cca2);
    
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});

// Función para obtener países vecinos NO CONSIGO ACCEDER A LOS DATOS POR LAS CORS :(
async function fetchNeighboringCountries(countryCode: string) {
  console.log(countryCode);
  
  try {
    const apiUrl = `https://api.geodatasource.com/neighbouring-countries?key=${apiKey}&country_code=${countryCode}`;
    const response = await fetch(apiUrl, { mode: 'no-cors' }); // Usar el modo 'no-cors'
    console.log('Response:', response); 
  } catch (error) {
    console.error('Error fetching neighboring countries:', error);
  }
}
</script>

<template>
  <div class="container mx-auto px-32 mt-5">
    <h1 class="font-bold text-3xl ">Lista de Paises</h1>
    <ul>
      <li class="flex my-5 gap-6 items-center" v-for="pais in data" :key="pais.name.common" @click="fetchNeighboringCountries(pais.cca2)">

        <img class="w-32" :src="pais.flags.png" :alt="pais.flags.alt">
        <h4> {{ pais.name.common }} </h4>
       
      </li>
    </ul>
    
    <h2>Países Vecinos</h2>
    <ul>
      <li v-for="vecino in neighboringCountries" :key="vecino.name.common">
        {{ vecino.name.common }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
