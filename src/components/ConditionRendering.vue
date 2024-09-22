<template>
  <div>
    <!-- v-if : Đc use khi khối lệnh cho có 1 điều kiện -->
    <h1 v-if="isShow">Hiển thị phần tử</h1>
    <h1 v-else>Ẩn phần tử</h1>
    <button @click="handleToggle">Toggle</button>
    <!-- v-if và v-else : đc use khi khối lệnh có 2  điều kiện -->
    <br />
    <br />
    <h1 v-if="age >= 18">Đủ tuổi thi</h1>
    <h1 v-else>Chưa đủ tuổi thi</h1>
    <h1>Tuổi : {{age}}</h1>
    <button @click="handleDecreaseAge">Giảm tuổi</button>
    <button @click="handleIncareaseAge">Tăng tuổi</button>
    <br />
    <!-- v-if, v-else-if, v-else : đc use khi khối lệnh có từ 3 điều kiện trở lên -->
    <h1 v-if="role === 'admin'">Quyền Admin</h1>
    <h1 v-else-if="role === 'user'">Quyền User</h1>
    <h1 v-else-if="role === 'edit'">Quyền Edit</h1>
    <h1 v-else>Quyền Other</h1>
    <!-- v-show : hiển thị dữ liệu có điều kiện , tuy nhiên là dữ liệu đó ko bị xóa khỏi DOM mà nó chỉ bị ẩn đi thông qua display:none-->
    <h1 v-show="isShowForm">Form content</h1>
  </div>
</template>

<script setup>
import { ref } from "vue";
const isShow = ref(true);
const age = ref(0);
const role = ref("user");
const isShowForm = ref(false);
const handleToggle = () => {
  isShow.value = !isShow.value;
};
// Tạo một biến tuổi . Nếu tuổi trên 18 thì sẽ hiển thị "Đủ tuổi thi" Ngược lại "Chua đủ tuổi thi"
// Hàm tăng tuổi
const handleIncareaseAge = () => {
  age.value++;
};
// Hàm giảm tuổi
const handleDecreaseAge = () => {
  age.value--;
};

// Tạo 1 biến có giá trị có thể là admin,user,edit,other
// Kiểm tra điều kiện và render ra tên quyền tương ứng
</script>

<style>
</style>