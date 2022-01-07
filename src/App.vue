<template>
  <div id="app">
    <h1 class="title is-1 has-text-white-ter">Pokédex</h1>
    <input type="text" class="column is-half is-offset-one-quarter input is-rounded" name="" id="" placeholder="Buscar pokémon pelo nome" v-model="find">
    <button id="btnFind" class="column is-half is-offset-one-quarter button is-info is-rounded" @click="findPokemon">Buscar</button>
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
    </div>
    </div>    
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      find: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    }).catch();
  },
  components: {
    Pokemon
  },
  methods: {
    findPokemon: function(){
      this.filteredPokemons = this.pokemons;

      if(this.find == '' || this.find == " "){
          this.filteredPokemons = this.pokemons;
        }else{
          this.filteredPokemons =  this.pokemons.filter(poke => poke.name == this.find.toLowerCase());
        }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: lightskyblue;
}

#btnFind{

  margin-top: 1%;
}
</style>
