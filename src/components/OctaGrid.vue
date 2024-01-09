<template>
  <div class="octagon-grid">
    <div v-for="row in rows" :key="row" class="octagon-row">
      <div
        v-for="col in columns"
        :key="col"
        class="octagon"
        :id="'octagon-' + dynamicId[counter]"
        :class="{ 'octagon-activated': isActive(dynamicId[row * col]) }"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: 5,
      columns: 10,
      activatedOctagons: [],
      counter: 0,
    };
  },
  computed: {
    dynamicId() {
      return this.columns > 0
        ? Array.from(
            { length: this.row * (this.columns + 1) },
            (_, index) => index
          )
        : [];
    },
  },
  methods: {
    isActive(index) {
      return this.activatedOctagons.includes(index);
    },
    activateOctagons() {
      this.activatedOctagons = [];
      const totalOctagons = this.rows * (this.columns + 1);
      const randomIndexes = [];
      while (randomIndexes.length < 10) {
        const randomIndex = Math.floor(Math.random() * totalOctagons);
        if (!randomIndexes.includes(randomIndex)) {
          randomIndexes.push(randomIndex);
        }
      }
      console.log(randomIndexes);
      randomIndexes.forEach((index, i) => {
        this.activatedOctagons.push(index);
        // setTimeout(() => {
        //   setTimeout(() => {
        //     this.activatedOctagons.splice(
        //       this.activatedOctagons.indexOf(index),
        //       1
        //     );
        //   }, 2000);
        // }, i * 2000);
      });
    },
  },
  mounted() {
    this.activateOctagons();
  },
};
</script>

<style lang="scss">
.octagon-grid {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  background-color: black;
}

.octagon-row {
  display: flex;
}

.octagon-activated {
  background-color: orange !important;
  filter: blur(40px) !important;
}

.octagon {
  width: 100px;
  height: 100px;
  margin: 7px;
  background-color: grey;
  filter: blur(100px);
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}
</style>
