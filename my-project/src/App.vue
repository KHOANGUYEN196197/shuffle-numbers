<template>
  <div class="shuffle">
    <div
      v-for="(item, index) of arrShuffle"
      :key="item"
      :class="item.isActive ? 'active' : ''"
      class="box-number"
      @click="changeActive(item, index)"
    >
      {{ item?.number }}
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      totalNumber: 300,
      arrShuffle: [],
      startNumber: 1,
    };
  },
  mounted() {
    this.handleArr();
  },
  methods: {
    handleArr() {
      let tempArr = [];
      for (let i = 0; i < this.totalNumber; i++) {
        const data = {
          number: i + 1,
          isActive: false,
        };
        tempArr.push(data);
      }
      this.arrShuffle = this.shuffle(tempArr);
      console.log(this.arrShuffle);
    },
    shuffle(array) {
      for (let i = array.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    },
    changeActive(item, index) {
      if (item.number === this.startNumber && !item.isActive) {
        this.arrShuffle[index].isActive = true;
        this.startNumber++;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.shuffle {
  display: flex;
  flex-wrap: wrap;
}
.box-number {
  background: black;
  padding: 3px;
  font-size: 35px;
  width: 60px;
  height: 40px;
  border-radius: 10px;
  color: #fff;
  margin-top: 15px;
  margin-right: 15px;
  cursor: default;
}
.active {
  background: red;
}
</style>
