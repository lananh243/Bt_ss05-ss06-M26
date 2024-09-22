<template>
  <div>
    <div class="but-container">
      <button @click="handleIncrease">Tăng dần</button>
      <button @click="handleDecrease">Giảm dần</button>
    </div>
    <br />
    <br />
    <div class="but-container">
      <button v-for="number in numbers" :key="number">{{ number }}</button>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const numbers = reactive([5, 3, 8, 1, 4, 7, 2, 6]);

const handleIncrease = () => {
  numbers.sort((a, b) => a - b);
};

const handleDecrease = () => {
  numbers.sort((a, b) => b - a);
};
</script>

<style scoped>
.but-container {
  display: flex;
  gap: 10px;
}
</style>