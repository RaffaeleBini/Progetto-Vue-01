<!-- App.vue -->
<template>
  <div class="app">
    <TicTacToe />
  </div>
</template>

<script lang="ts" setup>
import TicTacToe from './components/TicTacToe.vue'
</script>

<style>
.app {
  max-width: 800px;
  margin: 0 auto;
  text-align: center;
}

body {
  margin: 0;
  padding: 0;
  background-color: black;
}
</style>