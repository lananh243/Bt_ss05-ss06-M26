<template>
  <div>
    <ul v-for="user in listUser" :key="user.id">
      <li>
        <span>Id : {{user.id}}</span> -
        <span>Name : {{user.name}}</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
const listUser = [
  { id: 1, name: "Nguyễn Văn A" },
  { id: 2, name: "Nguyễn Văn B" }
];
</script>

<style>
</style>