<template>
  <div id="app"></div>
  <div class="column is-half is-offset-one-quarter">
    <div v-for="(poke, index) in pokemons" :key="index">
      <Pokemon :name="poke.name" :num="index + 1" :url="poke.url" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=15&offset=0")
      .then((data) => {
        this.pokemons = data.data.results;
      });
  },
  components: {
    Pokemon,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
