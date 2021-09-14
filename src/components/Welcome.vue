<template>
  <div class="welcome d-flex justify-content-center align-items-center">
    <slot></slot>
    <h3>{{ message }}</h3>
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: "Welcome",
  props: ["message"],
};
</script>

<style lang="scss" scoped>
.welcome {
  height: calc(100vh - 100px);
}
</style>
