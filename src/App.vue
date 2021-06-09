<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h3>POKEDEX</h3>
      <input class="input is-rounded" type="text" placeholder="Buscar Pokemon pelo nome" v-model="busca">
      <button class="button is-fullwidth" id="buscaBtn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1" />
      </div>
    </div>
  </div>
</template>
<script>
  import Pokemon from './components/Pokemon'
  import axios from 'axios';
  export default {
    name: 'App',
    data() {
      return {
        pokemons: [],
        filteredPokemons: [],
        busca: ''
      }
    },
    created: function () {
      axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
        console.log("Pegou a lista de pokemons!")
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
        console.log(this.pokemons)
      })
    },
    components: {
      Pokemon
    },
    methods: {
      buscar: function () {
        this.filteredPokemons = this.pokemons;
        if (this.busca == '' || this.busca == ' ') {
          this.filteredPokemons = this.pokemons;

        } else {
          this.filteredPokemons = this.pokemons.filter(Pokemon => Pokemon.name == this.busca);
        }
      }
    },
    computed: {
      /*
      resultadoBusca: function(){
        if(this.busca == '' || this.busca == ' '){
          return this.pokemons;
        }else{
          return this.pokemons.filter(Pokemon => Pokemon.name == this.busca)
        }
      }
      */
    }
  }
</script>

<style>
  #app 
  {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    background-color: #2c3e50;
    margin: 0;
    padding: 0;
  }
  #buscaBtn 
  {
    margin-top: 2%;
    background-color: rgb(141, 224, 198);
  }
</style>