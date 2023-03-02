<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">

      <h3 class="is-size-1" id="isText">POKÉDEX</h3>
      <input class="input is-rounded is-primary" type="text" placeholder="Buscar Pokemon pelo nome" v-model="busca">
      <button class="button is-fullwidth is-primary" id="isButton" @click="buscar">Buscar</button>
      <div v-for="(poke) in filteredPokemons" :key="poke.url" id="isDiv">
        <Pokemon :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  components: { Pokemon },
  name: 'App',
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0.').then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  componets: [
    Pokemon
  ],
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' | this.busca == ' '){
        this.filteredPokemons = this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca == '' | this.busca == ' '){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
    */
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #0e3d59;
}

#isButton {
  margin-top: 2%;
  margin-bottom: 4%;
}

#isText {
  margin-bottom: 2%;
}

</style>
