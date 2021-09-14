<template>
  <div id="app">
    <Header @search="find" :api="api" @filter="setFilter" />

    <main>
      <Welcome
        message="Trova i tuoi film preferiti con BoolFlix..."
        v-if="searching"
      >
        <i class="fas fa-film fa-2x fa-spin" />
      </Welcome>

      <div v-else>
        <Content title="Movies" :results="filtered('searchResult')" />
        <Content title="Series" :results="filtered('searchResultTv')" />
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";
import Welcome from "./components/Welcome.vue";

export default {
  name: "App",
  components: {
    Content,
    Header,
    Welcome,
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
      actualFilter: 0,
      searching: true,
    };
  },

  methods: {
    find(query) {
      // clean page if search empty
      console.log(query);
      if (query === " " || !query) {
        this.searchResult = [];
        this.searchResultTv = [];
        return;
      }

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
          this.searching = false;
        })
        .catch((err) => {
          console.log(err);
        });
    },

    setFilter(genre) {
      this.actualFilter = genre;
      console.log(this.actualFilter);
    },

    filtered(entity) {
      let result = this[entity];

      if (this.actualFilter == 0) {
        return result;
      }
      const filtered = result.filter((film) => {
        return film.genre_ids.includes(this.actualFilter);
      });

      return filtered;
    },
  },
};
</script>

<style lang="scss">
@import "./scss/style.scss";
</style>
