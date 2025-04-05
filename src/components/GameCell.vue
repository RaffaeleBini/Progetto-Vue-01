<template>
  <div
    class="cell"
    :class="{ filled: value !== '' }"
    @click="handleClick"
  >
    {{ value }}
  </div>
</template>

<script lang="ts" setup>
import { defineEmits, defineProps } from 'vue';

interface Props {
  value: string;
  row: number;
  col: number;
}
const props = defineProps<Props>();
const emit = defineEmits<{ (e: 'cell-clicked', row: number, col: number): void }>();

function handleClick() {
  if (props.value === '') {
    emit('cell-clicked', props.row, props.col);
  }
}
</script>

<style scoped>
.cell {
  width: 80px;
  height: 80px;
  border: 2px solid #333;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2em;
  cursor: pointer;
  transition: background-color 0.2s;
}
.cell:hover:not(.filled) {
  background-color: gold;
}
.filled {
  cursor: not-allowed;
}
</style>
