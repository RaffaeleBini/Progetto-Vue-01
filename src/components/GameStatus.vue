<template>
  <div class="game-info">
    <p>{{ message }}</p>
  </div>
</template>

<script lang="ts" setup>
import { defineProps } from 'vue';

interface Props {
  message: string;
}
const props = defineProps<Props>();
</script>

<style scoped>
.game-info {
  text-align: center;
  margin-top: 20px;
}
</style>
