<template>
  <div>
    <input
      type="text"
      placeholder="Cerca..."
      v-model.trim="searchText"
      @keyup.enter="emitSearch"
    />
    <button @click="emitSearch" class="my-3">
      Cerca
    </button>
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
  methods: {
    emitSearch() {
      this.$emit("search", this.searchText);
    },
  },
};
</script>

<style lang="scss" scoped></style>
