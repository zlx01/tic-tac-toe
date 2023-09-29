<template>
  <button class="square">
    {{ value }}
  </button>
</template>

<script setup>
defineProps({
  value: String,
});
</script>

<style scoped></style>
