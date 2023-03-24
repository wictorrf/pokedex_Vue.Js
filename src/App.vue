<template>
<div id="app">
  <nav class="navbar is-fixed-top is-dark"  role="navigation" aria-label="main navigation">
    <div class="navbar-brand">
      <a class="navbar-item" href="/">
        <img src="./assets/winsdev.png"/>
        <h1 class="is-size-4">Pokedex</h1>
      </a>
    </div>
  </nav>
  
  <div class="column is-half is-offset-one-quarter" id="main">
    <article class="panel is-dark">
    <p class="panel-heading">
      Buscar
    </p>
    
    <div class="panel-block" >
      <p class="control has-icons-left" id="buscar">
          <input class="input is-dark" type="text" placeholder="Buscar Pokemon pelo nome" v-model="busca">
          <button class="button is-dark" @click="buscar">Buscar</button>
      </p>
    </div>
  </article>
    <div id="cards" v-for="(poke,index) in filteredPokemons" :key="poke.url">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
    </div>
  </div>
</div>
</template>

<script>
import axios from "axios"
import Pokemon from "./components/PokemonComp.vue";

export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=150&offset=0").then(res => {
      console.log("Pegou a lista de pokemons!");
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filteredPokemons = this.pokemons;
      }else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
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
  margin-top: 100px;
  height: 100%;
}
#inicio{
  height: 6rem;
  margin-top: -40px;
}
#buscar{
  display: flex;
}
#main{
  margin: auto;
}
</style>
