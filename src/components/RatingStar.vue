<template>
  <div class="rating">
    <ul class="list">
      <li v-for="(star, index) in 5" :key="index" class="star">
        <i
          class="far fa-star"
          :class="rate(rating, index) ? 'fas fa-star' : ''"
        />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "RatingStar",
  props: ["rating"],
  methods: {
    rate(rating, index) {
      if (rating > index) {
        return true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
i {
  color: white;
}

.list {
  margin: 0 0 5px 0;
  padding: 0;
  list-style-type: none;
}

.star {
  display: inline-block;
  cursor: pointer;
}
</style>
