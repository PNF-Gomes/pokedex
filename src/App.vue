/* Pokedex Project 
Thank you for looking
Pedro Gomes

for the future:
instant search with auto complete
more data about pokemons
better visual
*/


<template>
  <div id="app">
    <img src="./assets/pokemon.jpg" alt="" />
    <br />
    <br />
    <!-- search input box that changes search variable value -->
    <md-input type="text" placeholder="Search Pokemon" v-model="search" />
   <!-- Button to call search function -->
    <button @click="searchF">Search</button>
    <!-- cicle for to generate all cards based on the pokemon array -->
    <div
      v-for="(poke, index) in filteredPokemons"
      :key="poke.url"
      class="columns"
    >
    <!-- Call for Pokemon component passing values given by the API-->
      <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
    </div>
    <hr />
    <p>Made by Pedro Gomes</p>
  </div>
</template>

<script>
/* Importing js library axios to work with http requests */
import axios from "axios";
/* Importing Pokemon card component */
import Pokemon from "./components/Pokemon";

export default {
  name: "App",
  data: function () {
    return {
      /* url for Pokemon api */
      url: "https://pokeapi.co/api/v2/pokemon?limit=151&offset=0",
      /* untouchable pokemons array */
      pokemons: [],
      /* pokemon array to filter search results */
      filteredPokemons: [],
      /* search variable to compare with names inside the array */
      search: "",
    };
  },
  created: function () {
    /* API calling  */
    axios.get(this.url).then((res) => {
      /* populating the array with API results */
      this.pokemons = res.data.results;
      /* debuging */
     /*  console.log(this.pokemons); */
     /* populating search array */
      this.filteredPokemons = this.pokemons;
    });
  },
  components: {
    /* declaring Pokemon card component */
    Pokemon,
  },
  methods: {
    /* Function  to compare results*/
    searchF: function () {
      /* returning untouchable array */
      if (this.search == "") {
        return (this.filteredPokemons = this.pokemons);
      } else {
        /* returning search results */
        return (this.filteredPokemons = this.pokemons.filter(
          (pokemon) => pokemon.name == this.search
        ));
      }
    },
  },
  /* Function to intant search on development*/
  computed: {
    /*  searchResults: function(){
      if(this.search == ""){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.search);
      }
    } */
  },
};
</script>

<style>
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
