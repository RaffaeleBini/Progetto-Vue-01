<template>
  <div class="board">
    <div v-for="(row, rowIndex) in board" :key="rowIndex" class="board-row">
      <Cell 
        v-for="(cell, colIndex) in row"
        :key="colIndex"
        :value="cell"
        :row="rowIndex"
        :col="colIndex"
        @cell-clicked="handleCellClick"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, } from 'vue';
import Cell from './GameCell.vue';

interface Props {
  board: string[][];
}

const props = defineProps<Props>();
const emit = defineEmits<{ (e: 'cell-clicked', row: number, col: number): void }>();

function handleCellClick(row: number, col: number) {
  emit('cell-clicked', row, col);
}
</script>

<style scoped>
.board {
  display: flex;
  flex-direction: column;
  margin: 20px 0;
  background-color: goldenrod;
}
.board-row {
  display: flex;
}
</style>
