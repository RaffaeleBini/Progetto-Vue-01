<template>
  <button class="reset-btn" @click="emitReset">Reset</button>
</template>

<script lang="ts" setup>
import { defineEmits } from 'vue';
const emit = defineEmits<{ (e: 'reset'): void }>();

function emitReset() {
  emit('reset');
}
</script>

<style scoped>
.reset-btn {
  padding: 10px 20px;
  font-size: 1em;
  background-color: goldenrod;
  color: black;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}
.reset-btn:hover {
  background-color: gold;
}
</style>
