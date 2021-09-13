<template>
  <div class="container-lg ">
    <section v-if="showSections()" class="row">
      <div
        class="col-6 col-lg-3"
        v-for="result in combinedResult"
        :key="result.id"
      >
        <Card
          :title="result.title || result.name"
          :originalTitle="result.original_title || result.original_name"
          :originalLanguage="result.original_language"
          :voteAverage="result.vote_average"
          :posterPath="result.poster_path"
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
  props: ["searchResult", "searchResultTv", "combinedResult"],
  methods: {
    showSections() {
      return !this.searchResult || !this.searchResultTv ? false : true;
    },
  },
};
</script>

<style scoped lang="scss"></style>
