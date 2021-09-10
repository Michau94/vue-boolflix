<template>
  <div class="container-lg">
    <section v-if="showSections()" class="row">
      <h2>Movies</h2>
      <div class="col-6" v-for="result in searchResult" :key="result.id">
        <Card
          :title="result.title"
          :originalTitle="result.original_title"
          :originalLanguage="result.original_language"
          :voteAverage="result.vote_average"
        />
      </div>
    </section>

    <section v-if="showSections()" class="row">
      <h2>Tv Series</h2>
      <div class="col-6" v-for="serie in searchResultTv" :key="serie.id">
        <Card
          :title="serie.name"
          :originalTitle="serie.original_name"
          :originalLanguage="serie.original_language"
          :voteAverage="serie.vote_average"
        />
      </div>
    </section>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "Content",
  components: {
    Card,
  },
  props: ["searchResult", "searchResultTv"],
  methods: {
    showSections() {
      return !this.searchResult || !this.searchResultTv ? false : true;
    },
  },
};
</script>

<style scoped lang="scss"></style>
