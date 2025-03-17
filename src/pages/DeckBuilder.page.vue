<template>
  <n-card v-for="pokemonItem in pokemon" :key="pokemonItem.name" title="Card with Cover">
    <template #cover>
      <img :src="pokemonItem.imageUrl" />
    </template>
    <div>
      <h3>{{ pokemonItem.name }}</h3>
      <p>Height: {{ pokemonItem.height }}</p>
      <p>Weight: {{ pokemonItem.weight }}</p>
      <p>Type : {{ pokemonItem.type.name }}</p>
      <p>Attaque : {{ pokemonItem.attack.name }}</p>
    </div>
  </n-card>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

// Define a ref to store the fetched Pokémon data (should be an array)
const pokemon = ref([]);

// Function to fetch Pokémon data
const getPokemon = async () => {
  try {
    const response = await axios.get('https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards');
    // Update the pokemon ref with the response data (should be an array of Pokémon)
    pokemon.value = response.data;
  } catch (error) {
    console.error('Erreur lors du chargement des pokemons :', error);
  }
};

// Fetch the Pokémon data when the component is mounted
onMounted(() => {
  getPokemon();
});
</script>

<style scoped>
.n-card {
  max-width: 200px;
}
</style>
