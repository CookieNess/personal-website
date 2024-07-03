<template>
  <div class="container">
    <div class="cookie"></div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.cookie {
  width: 100px;
  height: 100px;
  background-color: brown;
  // border-radius: 100%;
  position: relative;
  overflow: hidden;
  clip-path: polygon(
    0% 5%,
    5% 0%,
    95% 0%,
    100% 5%,
    100% 95%,
    95% 100%,
    5% 100%,
    0% 95%
  );
}
</style>
