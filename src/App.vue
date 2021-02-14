<template>
  <div class="container" id="app">
    <div class="columns mt-4">

      <div class="column is-half is-offset-one-quarter" align="center">

        <h1 class="title">Pokedex</h1>

      </div>

    </div>

    <div class="columns mt-1 mr-2 ml-2">

      <div class="column is-half is-offset-one-quarter" align="center">

        <input class="input is-primary" v-model="busca" type="text" placeholder="Buscar Pokemon pelo Nome">

      </div>

    </div>

    <div class="row">
      <div v-for="(pokemon, index) in resultadoBusca" :key="index">
        <Pokemon :nome="pokemon.name" :url="pokemon.url" :num="index+1" ></Pokemon>
      </div>
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
      pokemons: [],
      busca: ''
    }
  },
  created(){

    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((data) => {

      this.pokemons = data.data.results
      
    }).catch((err) => {
      console.log(err)
    })

  },
  computed: {
    resultadoBusca(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca.toLowerCase())
      }
    }
  }
}
</script>

<style scoped>
  button{
    width: 100%;
  }
</style>
