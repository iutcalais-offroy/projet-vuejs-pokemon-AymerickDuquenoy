<template>
  <input 
    type="text" 
    v-model="searchQuery" 
    placeholder="Rechercher un Pokémon par nom"
    class="search-input"
  />
  
  <div>
    <n-card v-for="pokemonItem in filteredPokemon" :key="pokemonItem.name">
      <template #cover>
        <img :src="pokemonItem.imageUrl" alt="Image de Pokémon" />
      </template>
      <h3>{{ pokemonItem.name }}</h3>
      <div class="info">
        <span class="pv">PV {{ pokemonItem.lifePoints }}</span>
        <n-tag 
          class="type" 
          :style="{ backgroundColor: getTypeColor(pokemonItem.type.name) }"
        >
          {{ pokemonItem.type.name }}
        </n-tag>
      </div>
      <h4>Taille: {{ pokemonItem.height }} | Poids: {{ pokemonItem.weight }}</h4>
      <n-tag class="attaque">
        {{ pokemonItem.attack.name }} {{ pokemonItem.attack.damages }}
      </n-tag>
    </n-card>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import axios from 'axios';

const pokemon = ref([]);
const searchQuery = ref('');

// Objet de mapping des couleurs en fonction des types
const typeColors = {
  fire: '#F08030',
  water: '#6890F0',
  grass: '#78C850',
  electric: '#F8D030',
  psychic: '#F85888',
  rock: '#B8A038',
  ghost: '#705898',
  dark: '#705848',
  steel: '#B8B8D0',
  dragon: '#7038F8',
  fairy: '#EE99AC',
  normal: '#A8A878',
  bug: '#A8B820',
  ice: '#98D8D8',
  fighting: '#C03028',
  poison: '#A040A0',
  ground: '#E0C068',
  flying: '#A890F0',
  unknown: '#6D6D6D',
  default: '#A0A0A0',
};

// Fonction pour récupérer la couleur du type
const getTypeColor = (type) => {
  return typeColors[type.toLowerCase()] || typeColors.default;
};

// Récupération des données Pokémon
const getPokemon = async () => {
  try {
    const response = await axios.get('https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards');
    pokemon.value = response.data;
  } catch (error) {
    console.error('Erreur lors du chargement des pokémons :', error);
  }
};

// Filtrage des Pokémon en fonction de la recherche
const filteredPokemon = computed(() => {
  if (!searchQuery.value.trim()) return pokemon.value;
  return pokemon.value.filter(pokemonItem =>
    pokemonItem.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

// Charger les Pokémon au montage du composant
onMounted(() => {
  getPokemon();
});
</script>

<style scoped>
.search-input {
  width: 100%;
  max-width: 300px;
  padding: 8px;
  margin: 20px auto;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  display: block;
}

.n-card {
  max-width: 200px;
  border: 1px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease-in-out;
  background: white;
}

.n-card:hover {
  transform: scale(1.05);
}

.n-card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

h3 {
  font-size: 18px;
  text-align: center;
  font-weight: bold;
  color: #333;
  margin: 10px 0;
}

h4 {
  font-size: 12px;
  text-align: center;
  color: #666;
  margin-top: 5px;
}

.pv {
  font-size: 14px;
  color: #e60000;
}

.info {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
}

.n-tag {
  font-size: 12px;
  padding: 5px 10px;
  color: white;
  font-weight: bold;
  text-transform: capitalize;
  border-radius: 12px;
}

.attaque {
  font-size: 14px;
  font-weight: bold;
  color: #333;
  display: block;
  text-align: center;
  margin-top: 10px;
}

div {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  margin-top: 20px;
}

.n-card {
  opacity: 0;
  animation: fadeIn 0.5s forwards;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
}
</style>
