<template>
  <img id="logo" src="./assets/pokemon-logo.png" />
  <div class="columns">
    <div class="column is-one-third">
      <div v-for="(pokemon, index) in pokemons1" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 1" />
      </div>
    </div>
    <div class="column is-one-third">
      <div v-for="(pokemon, index) in pokemons2" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 51" />
      </div>
    </div>
    <div class="column is-one-third">
      <div v-for="(pokemon, index) in pokemons3" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon.url" :num="index + 101" />
      </div>
    </div>
  </div>
</template>

<script>
import Pokemon from './components/Pokemon.vue';
import axios from 'axios';
export default {
  name: 'App',
  components: {
    Pokemon,
  },
  data() {
    return {
      pokemons1: [],
      pokemons2: [],
      pokemons3: []
    };
  },
  created: function () {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=50&offset=0').then((res) => {
      this.pokemons1 = res.data.results;
    });
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=50&offset=51').then((res) => {
      this.pokemons2 = res.data.results;
    });
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=50&offset=101').then((res) => {
      this.pokemons3 = res.data.results;
    })
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
  margin-top: 0;
  background-color: lightgray;
}

#logo {
  margin-top: 10px;
  max-width: 50%
}
</style>
