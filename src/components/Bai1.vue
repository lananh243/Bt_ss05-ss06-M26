<template>
  <div>
    <button @click="handleChange">{{isShow ? "Hiện" : "Ẩn"}}</button>

    <h2 v-if="isShow">Rikkei Education</h2>
  </div>
</template>

<script setup>
import { ref } from "vue";

const isShow = ref(true);

const handleChange = () => {
  isShow.value = !isShow.value;
};
</script>
