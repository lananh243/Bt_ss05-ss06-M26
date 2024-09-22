<template>
  <button @click="handleChange">{{isShow ? "Hiện" : "Ẩn"}}</button>
</template>

<script setup>
import { ref } from "vue";
const isShow = ref(true);

const handleChange = () => {
  isShow.value = !isShow.value;
};
</script>

<style>
</style>