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

<script setup>
import Board from "./Board.vue";
import { computed, ref } from "vue";

const history = ref([Array(9).fill(null)]);
const currentMove = ref(0);
const xIsNext = computed(() => currentMove.value % 2 === 0);
const currentSquares = computed(() => history.value[currentMove.value]);
function handlePlay(nextSquares) {
  history.value = [
    ...history.value.slice(0, currentMove.value + 1),
    nextSquares,
  ];
  currentMove.value = history.value.length - 1;
}

function jumpTo(nextMove) {
  currentMove.value = nextMove;
}
</script>

<style scoped></style>
