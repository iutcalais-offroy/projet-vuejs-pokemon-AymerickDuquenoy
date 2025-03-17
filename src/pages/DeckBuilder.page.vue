<template>
  <div>
    <n-card v-for="pokemonItem in pokemon" :key="pokemonItem.name">
      <template #cover>
        <img :src="pokemonItem.imageUrl" />
      </template>
      <h3>{{ pokemonItem.name }}</h3>
      <div class="info">
        <span class="pv">PV {{ pokemonItem.lifePoints }}</span>
        <n-tag class="type">{{ pokemonItem.type.name }}</n-tag>
      </div>
      <h4>Taille: {{ pokemonItem.height }} | Poids: {{ pokemonItem.weight }}</h4>
      <n-tag class="attaque"> {{ pokemonItem.attack.name }}  {{ pokemonItem.attack.damages}}</n-tag>
    </n-card>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const pokemon = ref([]);

const getPokemon = async () => {
  try {
    const response = await axios.get('https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards');
    pokemon.value = response.data;
  } catch (error) {
    console.error('Erreur lors du chargement des pokemons :', error);
  }
};

onMounted(() => {
  getPokemon();
});
</script>

<style scoped>
.n-card {
  max-width: 200px;
}
div {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}

h4 {
  font-size: 10px;
  text-align: center;
}

.attaque {
  font-size: 15px;
}

.pv {
  color: red;
}

.info {
  display: flex;
  align-items: center;
  gap: 10px;
}
</style>
