<template>
  <div id="app">
    <main-page/>
  </div>
</template>

<script>
import MainPage from "./components/MainPage.vue";

export default {
  name: "app",
  components: {
    MainPage
  }
};
</script>

<style lang="scss">
@import "./scss/styles.scss";
#app {
  @include font-face($font-serif);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  min-height: 100vh;
}
</style>
