<template>
  <div id="app">
    <div class="container">
      <h1>My pokedex</h1>
      <div class="pokemon-container">
        <PokemonCard v-for="pokemon in pokemons" :key="pokemon.name" :name="pokemon.name" :url="pokemon.url"/>
      </div>
    </div>
  </div>
</template>

<script>

import PokemonCard from './components/PokemonCard.vue'

export default {
  name: 'App',
  components: {
    PokemonCard
  },
  data(){
    return {
      pokemons: []
    }
  },
  created(){
    this.fetchPokemons()
  },
  methods: {
    async fetchPokemons() {
      const buscaPokemons = await fetch('https://pokeapi.co/api/v2/pokemon?limit=898&offset=0')
      const data = await buscaPokemons.json();
      this.pokemons = data.results
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Press Start 2P", display;
}
body {
    background-color: #cfffd0;
}
body::-webkit-scrollbar {
    width: 17px;
    
  }  
body::-webkit-scrollbar-thumb {
    border-radius: 10px;
    background-color: rgb(161, 255, 250);
  }
.container {
  background-color: #cfffd0;
  text-align: center;
  padding: 30px 20px;
}
.pokemon-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 50px 20px;
}
@media (max-width: 500px) {
  .pokemon-container {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  }
}
</style>
