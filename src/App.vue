<template>
    <div>
      <img src="./assets/title.png">
      <hr>
      <input @change="getSearch()" class="input is-rounded is-medium" type="text" placeholder="Busque pelo nome" v-model="search">
      <hr>
      <div v-for="poke in searchResult" :key="poke.url">
        <Pokemon
          :name="poke.name[0].toUpperCase() + poke.name.slice(1)"
          :url="poke.url"
          :num="poke.url.replace('https://pokeapi.co/api/v2/pokemon/', '').replace('/', '')"
        />
      </div>
    </div>
</template>

<script>
import Pokemon from "./components/Pokemon.vue";
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      search: ""
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log("Requisição ok");
        this.pokemons = res.data.results;
        this.onScreen = res.data.results;
      });
  },
  components: {
    Pokemon,
  },
  computed: {
    searchResult: function() {
      if (this.search == '' || this.search == ' ') {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name.includes(this.search.toLowerCase()));
      }
    }
  }
};
</script>

<style>
#app {
  background-color: aquamarine;
  padding-top: 20px;
  padding-bottom: 20px;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  min-height: 100vh;
}

hr {
  max-width: 400px;
}

input {
  width: 100%;
  max-width: 400px;
}
</style>
