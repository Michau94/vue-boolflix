<template>
  <div class="card-container">
    <div class="card" :style="{ backgroundImage: getImage() }">
      <div class="content overflow-auto">
        <div>
          Titolo:
          <h4>{{ title }}</h4>
        </div>
        <div>
          Titolo Originale:
          <h4>{{ originalTitle }}</h4>
        </div>
        <figure>
          Lingua:
          <img :src="getFlag(originalLanguage)" :alt="originalLanguage" />
        </figure>
        <RatingStar :rating="voteAverage" />
        <h5>Voto:{{ voteAverage }}</h5>
        <p>{{ overview }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import RatingStar from "./RatingStar.vue";
export default {
  data() {
    return {
      imgUrl:
        "url(https://www.altavod.com/assets/images/poster-placeholder.png)",
    };
  },
  name: "Card",
  components: {
    RatingStar,
  },
  props: [
    "title",
    "originalTitle",
    "originalLanguage",
    "voteAverage",
    "posterPath",
    "overview",
  ],
  methods: {
    getImage() {
      return this.posterPath == null
        ? "url(https://www.altavod.com/assets/images/poster-placeholder.png)"
        : "url(" + `https://image.tmdb.org/t/p/w500${this.posterPath}` + ")";
    },
    getFlag(originalLanguage) {
      return originalLanguage == "it" || originalLanguage == "en"
        ? require("../assets/images/" + originalLanguage + ".png")
        : null;
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/card.scss";
</style>
