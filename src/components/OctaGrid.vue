<template>
  <div class="octagon-grid">
    <div v-for="row in rows" :key="row" class="octagon-row">
      <div v-for="col in columns" :key="col" class="octagon"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: 11,
      columns: 25,
    };
  },
};
</script>

<style lang="scss">
.octagon-grid {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh; /* Full height of the viewport */
  overflow: hidden;
}

.octagon-row {
  display: flex;
}

.octagon {
  width: 100px; /* Adjust as needed */
  height: 100px; /* Adjust as needed */
  margin: 7px; /* Adjust as needed */
  transform: rotate(0deg);
  background-color: grey; /* Adjust as needed */
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}
</style>
