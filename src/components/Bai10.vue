<template>
  <div>
    <h2>{{numbers}}</h2>
    <button @click="handleRandom">Random number</button>

    <h3>Danh sách số nguyên trong mảng</h3>
    <div>
      <p v-for="number in numbers" :key="number.id">
        <span>{{number}}</span>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
const numbers = ref([]);
const handleRandom = () => {
  const random = Math.floor(Math.random() * 100);
  numbers.value = [...numbers.value, random];
};
</script>

<style>
</style>