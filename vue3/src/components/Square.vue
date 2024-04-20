<template>
  <button class="square" @click="$emit('click')">
    {{ value }}
  </button>
</template>

<script setup>
defineProps({
  value: String,
});
defineEmits(["click"]);
</script>

<style scoped></style>
