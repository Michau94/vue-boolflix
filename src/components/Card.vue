<template>
  <div class="card-container">
    <div
      class="card"
      :style="{
        backgroundImage: getImage(),
      }"
    >
      <div class="content overflow-auto">
        <h4>Titolo:{{ title }}</h4>
        <h5>Titolo Originale:{{ originalTitle }}</h5>
        <figure>
          Lingua:
          <img
            :src="
              originalLanguage == 'it' || originalLanguage == 'en'
                ? require('../assets/images/' + originalLanguage + '.png')
                : null
            "
            :alt="originalLanguage"
          />
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
      if (this.posterPath == null) {
        return "url(https://www.altavod.com/assets/images/poster-placeholder.png)";
      } else {
        return (
          "url(" + `https://image.tmdb.org/t/p/w500${this.posterPath}` + ")"
        );
      }
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/card.scss";
</style>
