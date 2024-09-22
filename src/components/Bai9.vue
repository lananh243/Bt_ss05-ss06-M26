<template>
  <div>
    <h2>Gender: {{ currentGender }}</h2>
    <button @click="handleRandomGender">Random gender</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

const genders = ["Nam", "Nữ", "Khác"];
const currentGender = ref(genders[0]);

const handleRandomGender = () => {
  const randomIndex = Math.floor(Math.random() * genders.length);
  currentGender.value = genders[randomIndex];
};
</script>

<style>
</style>