<template>
  <div>
    <div class="status">{{ status }}</div>
    <div class="board-row">
      <Square :value="squares[0]" @click.native="handleClick(0)" />
      <Square :value="squares[1]" @click.native="handleClick(1)" />
      <Square :value="squares[2]" @click.native="handleClick(2)" />
    </div>
    <div class="board-row">
      <Square :value="squares[3]" @click.native="handleClick(3)" />
      <Square :value="squares[4]" @click.native="handleClick(4)" />
      <Square :value="squares[5]" @click.native="handleClick(5)" />
    </div>
    <div class="board-row">
      <Square :value="squares[6]" @click.native="handleClick(6)" />
      <Square :value="squares[7]" @click.native="handleClick(7)" />
      <Square :value="squares[8]" @click.native="handleClick(8)" />
    </div>
  </div>
</template>

<script setup>
import Square from "./Square.vue";
import { computed } from "vue";

function calculateWinner(squares) {
  const lines = [
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    [0, 4, 8],
    [2, 4, 6],
  ];
  for (let i = 0; i < lines.length; i++) {
    const [a, b, c] = lines[i];
    if (squares[a] && squares[a] === squares[b] && squares[a] === squares[c]) {
      return squares[a];
    }
  }
  return null;
}

const props = defineProps({
  xIsNext: Boolean,
  squares: Array,
});

const emit = defineEmits(["play"]);

const status = computed(() => {
  const winner = calculateWinner(props.squares);
  if (winner) {
    return `Winner: ${winner}`;
  } else {
    return `Next player: ${props.xIsNext ? "X" : "O"}`;
  }
});

function handleClick(i) {
  if (calculateWinner(props.squares) || props.squares[i]) {
    return;
  }
  const nextSquares = props.squares.slice();
  if (props.xIsNext) {
    nextSquares[i] = "X";
  } else {
    nextSquares[i] = "O";
  }
  emit("play", nextSquares);
}
</script>

<style scoped></style>
