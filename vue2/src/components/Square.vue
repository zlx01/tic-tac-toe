<template>
  <button class="square" @click="$emit('click')">
    {{ value }}
  </button>
</template>

<script>
export default {
  name: "Square",
  props: {
    value: String,
  },
};
</script>

<style scoped></style>
