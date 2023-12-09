<template>
  <div id="app"></div>
  <h4 class="is-size-4">Pokedex</h4>
  <div class="column is-half is-offset-one-quarter">
    <input
      type="text"
      placeholder="Buscar pokemon pelo nome"
      v-model="busca"
      class="input is-rounded"
    />
    <button
      class="button is-fullwidth is-success"
      id="buscarBtn"
      @click="buscar"
    >
      Buscar
    </button>
    <div v-for="(poke, index) in filterPokemons" :key="poke.url">
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
      filterPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=15&offset=0")
      .then((data) => {
        this.pokemons = data.data.results;
        this.filterPokemons = data.data.results;
      });
  },
  methods: {
    buscar: function () {
      if (this.busca === "") {
        this.filterPokemons = this.pokemons; 
      } else {
        const buscaMinuscula = this.busca.toLowerCase(); 
        this.filterPokemons = this.pokemons.filter((pokemon) =>
          pokemon.name.toLowerCase().includes(buscaMinuscula)
        );
      }
    },
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

#buscarBtn {
  margin-top: 2%;
}
</style>
