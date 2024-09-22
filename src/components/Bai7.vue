<template>
  <div class="container">
    <button :class="{ active: activeIndex === 1 }" @click="setActive(1)">Button 1</button>
    <button :class="{ active: activeIndex === 2 }" @click="setActive(2)">Button 2</button>
    <button :class="{ active: activeIndex === 3 }" @click="setActive(3)">Button 3</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
const activeIndex = ref(1);

const setActive = index => {
  activeIndex.value = index;
};
</script>

<style scoped>
.container {
  display: flex;
  gap: 30px;
}
button {
  height: 35px;
  width: 100px;
}
.active {
  background-color: red;
  color: #fff;
}
</style>