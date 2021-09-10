<template>
  <div>
    <input
      type="text"
      placeholder="Cerca..."
      v-model="searchText"
      @keyup="$emit('search', searchText)"
    />
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      searchText: "",
    };
  },
};
</script>

<style lang="scss" scoped></style>
