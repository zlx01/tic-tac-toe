<template>
  <div class="game">
    <div class="game-board">
      <Board :xIsNext="xIsNext" :squares="currentSquares" @play="handlePlay" />
    </div>
    <div class="game-info">
      <ol>
        <li v-for="(squares, move) in history" :key="move">
          <button @click="jumpTo(move)">
            {{ move ? `Go to move #${move}` : "Go to game start" }}
          </button>
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
import Board from "./Board.vue";
export default {
  name: "Game",
  components: {
    Board,
  },
  data() {
    return {
      history: [Array(9).fill(null)],
      currentMove: 0,
    };
  },
  computed: {
    xIsNext() {
      return this.currentMove % 2 === 0;
    },
    currentSquares() {
      return this.history[this.currentMove];
    },
  },
  methods: {
    handlePlay(nextSquares) {
      this.history = [
        ...this.history.slice(0, this.currentMove + 1),
        nextSquares,
      ];
      this.currentMove = this.history.length - 1;
    },
    jumpTo(nextMove) {
      this.currentMove = nextMove;
    },
  },
};
</script>

<style scoped></style>
