<template>
  <button class="square">
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
