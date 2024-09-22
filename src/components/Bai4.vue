<template>
  <div>
    <button @click="handleDisplay">Hiển thị</button>
    <button @click="handleHidden">Ẩn</button>
    <h3 v-show="isShow">Thông báo : Welcome to Rikkei Education</h3>
  </div>
</template>

<script setup>
import { ref } from "vue";
const isShow = ref(true);
const handleHidden = () => {
  isShow.value = false;
};
const handleDisplay = () => {
  isShow.value = true;
};
</script>

<style>
</style>