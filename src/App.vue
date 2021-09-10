<template>
  <div id="app">
    <Search @search="search" />
    <button @click="find">Cerca</button>

    <!-- pseudo card  componente to be -->

    <div class="card" v-for="result in searchResult" :key="result.id">
      <h3 class="text-dark">{{ result.title }}</h3>
      <h5>{{ result.original_title }}</h5>
      <h5>{{ result.original_language }}</h5>
      <h5>{{ result.vote_average }}</h5>
      <figure></figure>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Search from "./components/Search.vue";

export default {
  name: "App",
  components: {
    Search,
  },
  data() {
    return {
      searchResult: [],
      searchText: " ",
    };
  },

  // da trasformare in funzione al keyup
  methods: {
    find() {
      const apikey = "cde3eaa50ec9e14e90a124f80a98153d";
      const baseUri = "https://api.themoviedb.org/3";

      // clean page in search empty
      if (this.searchText === " " || !this.searchText) {
        this.searchResult = [];
      } else {
        axios
          .get(
            `${baseUri}/search/movie?api_key=${apikey}&query=${this.searchText}`
          )
          .then((res) => {
            this.searchResult = res.data.results;
            console.log(this.searchResult);
          })
          .catch((err) => {
            console.log(err);
          });
      }
    },
    search(text) {
      this.searchText = text;
    },
  },
};
</script>

<style lang="scss">
@import "./scss/style.scss";
</style>
