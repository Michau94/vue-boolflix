<template>
  <div class="d-flex align-items-center mx-2 flex-wrap">
    <input
      type="text"
      placeholder="Cerca..."
      v-model.trim="searchText"
      @keyup.enter="emitSearch"
    />
    <div @click="emitSearch" class="mx-3 btn btn-light">
      Cerca
    </div>
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
      this.searchText = " ";
    },
  },
};
</script>

<style lang="scss" scoped></style>
