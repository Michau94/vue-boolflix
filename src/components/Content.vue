<template>
  <div class="container-md h-100">
    <section class="row m-3" v-if="results.length > 0">
      <h2 class="text-white p-4">{{ title }}</h2>
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
    <h4
      v-else
      class="text-light d-flex justify-content-center align-items-center"
    >
      No Mathces Found!
    </h4>
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
