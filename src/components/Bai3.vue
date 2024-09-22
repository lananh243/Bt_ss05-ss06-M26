<template>
  <div>
    <h3 v-if="userRole === 'admin'">Quyền hạn của bạn là : Admin</h3>
    <h3 v-else-if="userRole === 'user'">Quyền hạn của bạn là : User</h3>
    <h3 v-else-if="userRole === 'guest'">Quyền hạn của bạn là : Guest</h3>
  </div>
</template>

<script setup>
import { ref } from "vue";
const userRole = ref("admin");
</script>

<style>
</style>