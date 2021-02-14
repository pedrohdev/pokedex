<template>
  <div id="app">
    <div v-for="(pokemon, index) in pokemons" :key="index">
      <Pokemon :nome="pokemon.name" :url="pokemon.url" :num="index+1" ></Pokemon>
    </div>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Pokemon
  },
  data(){
    return {
      pokemons: []
    }
  },
  created(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((data) => {
      this.pokemons = data.data.results
      
    }).catch((err) => {
      console.log(err)
    })
  }
}
</script>

<style>

</style>
