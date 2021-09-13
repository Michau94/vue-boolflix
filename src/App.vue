<template>
  <div id="app">
    <header
      class="container-flex d-flex align-items-center justify-content-around"
    >
      <h2 class="text-light">Boolflix</h2>

      <div class="d-flex align-items-center">
        <Search @search="find" />
      </div>
    </header>

    <Content
      :searchResult="searchResult"
      :searchResultTv="searchResultTv"
      :combinedResult="combinedResult"
    />
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
      api: {
        baseUri: "https://api.themoviedb.org/3/",
        apikey: "cde3eaa50ec9e14e90a124f80a98153d",
      },
    };
  },

  // da trasformare in funzione al keyup
  methods: {
    find(query) {
      // clean page if search empty
      if (query === " " || !query) {
        this.searchResult = [];
        this.searchResultTv = [];
        return;
      }

      // MOVIES REQUEST

      this.fetchApi(query, "search/movie", "searchResult");
      this.fetchApi(query, "search/tv", "searchResultTv");
    },

    fetchApi(query, endpoint, entity) {
      const params = {
        params: {
          query,
          api_key: this.api.apikey,
          language: "it-IT",
        },
      };
      axios
        .get(`${this.api.baseUri}${endpoint}`, params)
        .then((res) => {
          this[entity] = res.data.results;
          console.log(this.searchResult);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },

  computed: {
    combinedResult() {
      return [...this.searchResult, ...this.searchResultTv];
    },
  },
};
</script>

<style lang="scss">
@import "./scss/style.scss";
</style>
