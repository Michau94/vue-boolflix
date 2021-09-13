<template>
  <div>
    <div
      class="card"
      :style="{
        backgroundImage:
          'url(' + `https://image.tmdb.org/t/p/w500${posterPath}` + ')',
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
        <h5>Voto:{{ Math.ceil(voteAverage / 2) }}</h5>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: [
    "title",
    "originalTitle",
    "originalLanguage",
    "voteAverage",
    "posterPath",
  ],
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

  img {
    width: 40px;
  }
}

.content {
  height: 100%;
  width: 100%;
  padding: 10px;
  background-size: cover;
  border-radius: 15px;
  background-repeat: no-repeat;
  background-position: center;
  opacity: 0;
  color: white;

  &:hover {
    opacity: 1;
    background: linear-gradient(rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0.8));
  }
}
</style>
