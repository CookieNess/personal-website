<template>
  <div id="app">
    <OctaGrid />
  </div>
</template>

<script>
import OctaGrid from "./components/OctaGrid.vue";
export default {
  name: "app",
  components: {
    OctaGrid,
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
