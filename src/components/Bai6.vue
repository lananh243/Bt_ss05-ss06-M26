<template>
  <div>
    <h2>Danh sách các số thỏa mãn điều kiện</h2>
    <div v-for="(number,index) in evenNumber()" :key="index">
      <b>{{number}}</b>
    </div>
  </div>
</template>

<script setup>
import { reactive } from "vue";

const number = reactive([5, 12, 15, 22, 9, 18, 25, 30, 7, 33]);
const evenNumber = () => {
  const filterNumber = number.filter(
    item => item % 2 !== 0 && item % 3 === 0 && item > 10
  );
  return filterNumber;
};
</script>

<style>
</style>