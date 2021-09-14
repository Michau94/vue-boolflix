<template>
  <div class="container-md">
    <section class="row m-3">
      <h2 class="text-white">{{ title }}</h2>
      <div
        class="col-xs-12 col-sm-6 col-md-4 col-lg-3 col-lg-2"
        v-for="result in results"
        :key="result.id"
      >
        <Card
          :title="result.title || result.name"
          :originalTitle="result.original_title || result.original_name"
          :originalLanguage="result.original_language"
          :voteAverage="getRating(result.vote_average)"
          :posterPath="result.poster_path"
          :overview="result.overview || 'No Overview...'"
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
  props: ["results", "title"],
  methods: {
    getRating(vote) {
      return Math.ceil(vote / 2);
    },
  },
};
</script>

<style scoped lang="scss"></style>
