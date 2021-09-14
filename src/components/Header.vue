<template>
  <header
    class="container-flex d-flex align-items-center justify-content-between"
  >
    <h2 class="px-5">Boolflix</h2>

    <div class="d-flex align-items-center flex-wrap">
      <select v-model="selectedGenre" @change="$emit('filter', selectedGenre)">
        <option value="0">Tutti</option>
        <option :value="genre.id" v-for="(genre, idx) in genres" :key="idx">{{
          genre.name
        }}</option>
      </select>
      <Search @search="emitQuery" />
    </div>
  </header>
</template>

<script>
import axios from "axios";
import Search from "./Search.vue";
export default {
  name: "Header",
  components: {
    Search,
  },
  props: ["api"],
  data() {
    return {
      genres: [],
      selectedGenre: 0,
    };
  },
  created() {
    axios
      .get(
        `${this.api.baseUri}genre/movie/list?api_key=${this.api.apikey}&language=it`
      )
      .then((res) => {
        this.genres = res.data.genres;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    emitQuery(query) {
      this.$emit("search", query);
    },
  },
};
</script>

<style></style>
