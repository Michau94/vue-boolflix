<template>
  <div>
    <div class="card">
      <h4>{{ title }}</h4>
      <h5>{{ originalTitle }}</h5>
      <h5>{{ originalLanguage }}</h5>
      <h5>{{ voteAverage }}</h5>
      <figure>
        <img
          :src="
            originalLanguage == 'it' || originalLanguage == 'en'
              ? require('../assets/images/' + originalLanguage + '.png')
              : null
          "
          :alt="originalLanguage"
        />
      </figure>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["title", "originalTitle", "originalLanguage", "voteAverage"],
};
</script>

<style scoped lang="scss">
.card {
  height: 500px;
  padding: 30px;

  img {
    width: 40px;
  }
}
</style>
