<template>
  <div>
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
.card {
  height: 500px;
  position: relative;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  margin: 10px;
  border-radius: 15px;
  overflow: hidden;

  img {
    width: 40px;
  }
  .content {
    height: 100%;
    width: 100%;
    padding: 10px;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center;
    opacity: 0;
    color: white;

    &:hover {
      opacity: 1;
      background: linear-gradient(rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.8));
    }
  }
}
</style>
