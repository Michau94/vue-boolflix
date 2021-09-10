<template>
  <div id="app">
    <header
      class="container-flex d-flex align-items-center justify-content-between"
    >
      <h2 class="text-light">Boolflix</h2>

      <div class="d-flex align-items-center">
        <Search @search="search" />
        <button @click="find" class="my-3">Cerca</button>
      </div>
    </header>

    <Content :searchResult="searchResult" :searchResultTv="searchResultTv" />
  </div>
</template>

<script>
import axios from "axios";
import Search from "./components/Search.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Search,
    Content,
  },
  data() {
    return {
      searchResult: [],
      searchResultTv: [],
      searchText: " ",
    };
  },

  // da trasformare in funzione al keyup
  methods: {
    find() {
      const apikey = "cde3eaa50ec9e14e90a124f80a98153d";
      const baseUri = "https://api.themoviedb.org/3";

      // clean page if search empty
      if (this.searchText === " " || !this.searchText) {
        this.searchResult = [];
        this.searchResultTv = [];
      } else {
        // MOVIES REQUEST
        axios
          .get(
            `${baseUri}/search/movie?api_key=${apikey}&language=it&query=${this.searchText}`
          )
          .then((res) => {
            this.searchResult = res.data.results;
            console.log(this.searchResult);
          })
          .catch((err) => {
            console.log(err);
          });

        // TV SERIES REQUEST
        axios
          .get(
            `${baseUri}/search/tv?api_key=${apikey}&language=it&query=${this.searchText}`
          )
          .then((res) => {
            this.searchResultTv = res.data.results;
            console.log(this.searchResultTv);
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
