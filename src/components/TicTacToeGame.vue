<template>
  <div class="game-container">
    <h1>Tic Tac Toe</h1>
    <Board :board="board" @cell-clicked="handleCellClick" />
    <GameStatus :message="statusMessage" />
    <ResetButton @reset="resetGame" />
  </div>
</template>

<script lang="ts" setup>
import { ref, computed } from 'vue';
import Board from './GameBoard.vue';
import GameStatus from './GameStatus.vue';
import ResetButton from './ResetButton.vue';

// Initialize a 3x3 board filled with empty strings
function createEmptyBoard() {
  return Array.from({ length: 3 }, () => Array(3).fill(''));
}

const board = ref<string[][]>(createEmptyBoard());
const currentPlayer = ref('X');
const winner = ref<string | null>(null);

function handleCellClick(row: number, col: number) {
  // Do nothing if cell is already set or if the game is already won.
  if (board.value[row][col] !== '' || winner.value) return;

  // Set the cell to the current player's symbol.
  board.value[row][col] = currentPlayer.value;

  // Check if the current move wins the game.
  if (checkWin(currentPlayer.value)) {
    winner.value = currentPlayer.value;
  } else {
    // Switch players if no win (simple two-player alternate)
    currentPlayer.value = currentPlayer.value === 'X' ? 'O' : 'X';
  }
}

function checkWin(player: string): boolean {
  // Check rows, columns, and diagonals for a win.
  const b = board.value;

  // Check rows
  for (let i = 0; i < 3; i++) {
    if (b[i].every(cell => cell === player)) return true;
  }
  // Check columns
  for (let j = 0; j < 3; j++) {
    if (b[0][j] === player && b[1][j] === player && b[2][j] === player) return true;
  }
  // Check diagonals
  if (b[0][0] === player && b[1][1] === player && b[2][2] === player) return true;
  if (b[0][2] === player && b[1][1] === player && b[2][0] === player) return true;

  return false;
}

function resetGame() {
  board.value = createEmptyBoard();
  currentPlayer.value = 'X';
  winner.value = null;
}

const statusMessage = computed(() => {
  if (winner.value) {
    return `Player ${winner.value} wins!`;
  } else {
    return `It's ${currentPlayer.value}'s turn`;
  }
});
</script>

<style scoped>
h1, p {
  color: gold;
}

.game-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  font-family: 'Segoe UI', Verdana, sans-serif;
  color: white;
}

/*.board {
  display: flex;
  flex-direction: column;
  margin: 20px 0;
  background-color: goldenrod;
}

.board-row {
  display: flex;
}

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

.game-info {
  text-align: center;
  margin-top: 20px;
}

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
}*/
</style>