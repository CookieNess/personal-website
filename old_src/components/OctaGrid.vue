<template>
  <div class="octagon-grid">
    <div v-for="(row, rowIndex) in rows" :key="rowIndex" class="octagon-row">
      <div
        v-for="(col, colIndex) in columns"
        :key="colIndex"
        :class="{ 'octagon-activated': isActivated(rowIndex, colIndex) }"
        :id="'octagon-' + getOctagonId(rowIndex, colIndex)"
        :style="{ 'background-color': getOctagonColor(rowIndex, colIndex) }"
        class="octagon"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      rows: 5,
      columns: 5,
      activatedOctagons: [],
    };
  },
  methods: {
    getOctagonId(rowIndex, colIndex) {
      return rowIndex * this.columns + colIndex + 1;
    },
    getOctagonColor(rowIndex, colIndex) {
      const octagonId = this.getOctagonId(rowIndex, colIndex);
      const isActivated = this.activatedOctagons.includes(octagonId);

      if (isActivated) {
        return Math.random() < 0.5 ? "orange" : "purple";
      }
    },
    isActivated(rowIndex, colIndex) {
      const octagonId = this.getOctagonId(rowIndex, colIndex);
      return this.activatedOctagons.includes(octagonId);
    },
    activateRandomOctagons() {
      const totalOctagons = this.rows * this.columns;
      const randomIndices = [];

      setInterval(() => {
        if (randomIndices.length === 10) {
          return;
        }
        const randomIndex = Math.floor(Math.random() * totalOctagons);
        if (!randomIndices.includes(randomIndex)) {
          randomIndices.push(randomIndex);
          this.activatedOctagons.push(randomIndex + 1);
        }
      }, 200);
    },
  },
  created() {
    this.activateRandomOctagons();
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
  filter: blur(40px) !important;
  animation: fade 2s forwards;
}

.octagon {
  width: 100px;
  height: 100px;
  margin: 7px;
  background-color: black;
  filter: blur(100px);
  clip-path: polygon(50% 0%, 100% 25%, 100% 75%, 50% 100%, 0% 75%, 0% 25%);
}

@keyframes fade {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}
</style>
