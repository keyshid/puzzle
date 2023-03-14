<template>
  <div id="app">
    <div class="home">
      <table>
        <tbody>
          <tr v-for="(items, row) in board" :key="row">
            <td
              v-for="(item, col) in items"
              :key="col"
              @click="swapBoard(row, col)"
            >
              {{ item }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import {
  createBoard,
  mixBoard,
  isSwappable,
  getSwappableIndexes,
  swap,
  isCorretBoard,
} from "../src/helper";
export default {
  name: "App",
  components: {},
  data() {
    return {
      size: 4,
      board: [],
      childBoard: [],
    };
  },
  methods: {
    swapBoard(items, item) {
      if (isSwappable(this.board, [items, item])) {
        const indexes = getSwappableIndexes(this.board, [items, item]);
        this.board = swap(this.board, indexes[0], indexes[1]);
      }
      if (isCorretBoard(this.board)) {
        alert("u win .");
      }
    },
  },
  created() {
    this.board = createBoard(this.size);
    this.board = mixBoard(this.board, 1000);
  },
};
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  width: 100%;
  height: 100vh;
}
.home {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100%;
  td {
    width: 100px;
    height: 100px;
    font-size: 40px;
    color: #2c3e50;
    border: 2px solid black;
    text-align: center;
    -webkit-user-select: none;
    user-select: none;
    transition: 1s ease-in-out;
  }
  :hover {
    cursor: pointer;
  }
}
</style>
