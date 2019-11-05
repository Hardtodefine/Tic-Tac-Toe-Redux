<template>
  <div id="app">
    <div>第{{n}}手</div>
    <div id="column">
      <Cell @click="onClickCell(1,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(2,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(3,$event)" v-bind:n="n"></Cell>
    </div>
    <div id="column">
      <Cell @click="onClickCell(4,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(5,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(6,$event)" v-bind:n="n"></Cell>
    </div>
    <div id="column">
      <Cell @click="onClickCell(7,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(8,$event)" v-bind:n="n"></Cell>
      <Cell @click="onClickCell(9,$event)" v-bind:n="n"></Cell>
    </div>
    结果:{{rst === undefined ? '胜负未分':`胜方为${rst}`}}
  </div>
</template>
<script>
import Cell from "./Cell";
export default {
  data() {
    return {
      n: 0,
      map: [[null, null, null], [null, null, null], [null, null, null]],
      result: []
    };
  },
  computed: {
    rst() {
      return (this.result[0]);
    }
  },
  methods: {
    onClickCell(i, text) {
      i = i - 1;
      console.log(`${i}个,内容${text}`);
      this.map[Math.floor(i / 3)][i % 3] = text;
      this.n = this.n + 1;
      this.tell();
    },
    tell() {
      const map = this.map;
        if (
          map[0][0] !== null && map[0][0] === map[1][1] && map[1][1] === map[2][2]
        ) {
          this.result.push(map[0][0]);
        }
        if (
          map[2][0] !== null && map[0][2] === map[1][1] && map[1][1] === map[2][0]
        ) {
          this.result.push(map[0][2]);
        }
      // for (let i = 0; i < 2; i++) {
        for (let i = 0; i < 3; i++) {
          if (
            map[i][0] !== null &&
            map[i][0] === map[i][1] &&
            map[i][1] === map[i][2]
          ) {
            this.result.push(map[i][0]);
          }
        }
        for (let j = 0; j < 3; j++) {
          if (
            map[0][j] !== null &&
            map[0][j] === map[1][j] &&
            map[1][j] === map[2][j]
          ) {
            this.result.push(map[0][j]);
            return;
          }
        }
      // }
    }
  },
  components: { Cell }
};
</script>
<style>
#app {
  position: absolute;
  display: flex;
  left: 50%;
  top: 50%;
  margin-left: -150px;
  margin-top: -150px;
}
</style>