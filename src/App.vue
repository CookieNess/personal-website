<template>
  <div id="app">
    <CookieAnimation />
  </div>
</template>

<script>
import CookieAnimation from "./components/CookieAnimation.vue";
export default {
  name: "app",
  components: {
    CookieAnimation,
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
#app {
  text-align: center;
  margin: 0;
  padding: 0;
}
</style>
