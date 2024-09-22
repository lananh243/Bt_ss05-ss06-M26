<template>
  <div>
    <div v-for="(num,index) in evenNumbers()" :key="index">
      <b>{{num}}</b>
    </div>
  </div>
</template>

<script setup>
import { reactive, computed } from "vue";

const array = reactive([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);

const evenNumbers = () => {
  const filterNumbers = array.filter(item => item % 2 === 0);
  return filterNumbers;
};
</script>

<style>
</style>