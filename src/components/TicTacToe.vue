<template>
    <div class="game-container">
      <h1>Tic Tac Toe</h1>
      
      <div class="board">
        <div v-for="(row, rowIndex) in board" 
             :key="rowIndex" 
             class="board-row">
          <div v-for="(cell, colIndex) in row" 
               :key="colIndex" 
               class="cell"
               :class="{ filled: cell !== null }"
               @click="makeMove(rowIndex, colIndex)">
            {{ cell }}
          </div>
        </div>
      </div>
  
      <div class="game-info">
        <p v-if="winner">Winner: {{ winner }}</p>
        <p v-else-if="isDraw">Game Draw!</p>
        <p v-else>Current Player: {{ currentPlayer }}</p>
        <button @click="resetGame" class="reset-btn">Reset Game</button>
      </div>
    </div>
</template>
  
<script>
  export default {
    name: 'TicTacToe',
    data() {
      return {
        board: Array(3).fill().map(() => Array(3).fill(null)),
        currentPlayer: 'X',
        winner: null,
        isDraw: false
      }
    },
    methods: {
      makeMove(row, col) {
        // If cell is already filled or game is over, return
        if (this.board[row][col] || this.winner || this.isDraw) {
          return;
        }
  
        // Make the move
        this.board[row][col] = this.currentPlayer;
  
        // Check for winner
        if (this.checkWinner()) {
          this.winner = this.currentPlayer;
          return;
        }
  
        // Check for draw
        if (this.checkDraw()) {
          this.isDraw = true;
          return;
        }
  
        // Switch player
        this.currentPlayer = this.currentPlayer === 'X' ? 'O' : 'X';
      },
  
      checkWinner() {
        // Check rows
        for (let i = 0; i < 3; i++) {
          if (this.board[i][0] && 
              this.board[i][0] === this.board[i][1] && 
              this.board[i][0] === this.board[i][2]) {
            return true;
          }
        }
  
        // Check columns
        for (let i = 0; i < 3; i++) {
          if (this.board[0][i] && 
              this.board[0][i] === this.board[1][i] && 
              this.board[0][i] === this.board[2][i]) {
            return true;
          }
        }
  
        // Check diagonals
        if (this.board[0][0] && 
            this.board[0][0] === this.board[1][1] && 
            this.board[0][0] === this.board[2][2]) {
          return true;
        }
        
        if (this.board[0][2] && 
            this.board[0][2] === this.board[1][1] && 
            this.board[0][2] === this.board[2][0]) {
          return true;
        }
  
        return false;
      },
  
      checkDraw() {
        return this.board.every(row => row.every(cell => cell !== null));
      },
  
      resetGame() {
        this.board = Array(3).fill().map(() => Array(3).fill(null));
        this.currentPlayer = 'X';
        this.winner = null;
        this.isDraw = false;
      }
    }
  }
</script>
  
<style scoped>
  h1,p {
    color: gold;
  }

  .game-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
    font-family: 'Segoe UI', Verdana, sans-serif;
  }
  
  .board {
    display: flex;
    flex-direction: column;
    margin: 20px 0;
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
  }
</style>