<template>
  <div id="app">
    <Search @search="search" />
    <button @click="find">Cerca</button>

    <!-- pseudo card  componente to be -->

    <div class="card" v-for="result in searchResult" :key="result.id">
      <h4>{{ result.title }}</h4>
      <h5>{{ result.original_title }}</h5>
      <h5>{{ result.original_language }}</h5>
      <h5>{{ result.vote_average }}</h5>

      <img
        :src="
          result.original_language == 'it' || result.original_language == 'en'
            ? require('./assets/images/' + result.original_language + '.png')
            : null
        "
        :alt="result.original_language"
      />
    </div>
    <h2>TV Series</h2>

    <!-- tv series result -->
    <div class="card" v-for="serie in searchResultTv" :key="serie.id">
      <h4>{{ serie.name }}</h4>
      <h5>{{ serie.original_name }}</h5>
      <h5>{{ serie.original_language }}</h5>
      <h5>{{ serie.vote_average }}</h5>

      <img
        :src="
          serie.original_language == 'it' || serie.original_language == 'en'
            ? require('./assets/images/' + serie.original_language + '.png')
            : null
        "
        :alt="serie.original_language"
      />
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
