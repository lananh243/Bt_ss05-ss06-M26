<template>
  <div class="container">
    <!-- Modal chỉnh sửa công việc -->
    <div v-if="showEditModal" class="custom-modal">
      <div class="modal-content">
        <span class="close" @click="closeModal">&times;</span>
        <h2>Chỉnh sửa công việc</h2>
        <label for="job-name">Tên công việc</label>
        <br />
        <br />
        <input id="job-name" v-model="editJob.name" type="text" class="input" />
        <div class="close_save">
          <div></div>
          <div class="modalBtn">
            <button @click="closeModal" class="but">Close</button>
            <button @click="handleSaveEdit" class="button">Save</button>
          </div>
        </div>
      </div>
    </div>
    <div class="todo">
      <h3 class="heading">Danh sách công việc</h3>
      <form @submit.prevent="handleAddJob" class="header">
        <input v-model="inputValue" type="text" class="input" />
        <button type="submit" class="button button-add">Add job</button>
      </form>

      <ul class="list-item" v-for="item in listJob" :key="item.id">
        <li class="item">
          <div class="left">
            <input
              @change="handleUpdateStatus(item.id)"
              v-bind:checked="item.status"
              type="checkbox"
              :id="item.name"
            />
            <label
              :style="{textDecoration : item.status ? 'line-through' : 'none'}"
              :for="item.name"
            >{{item.name}}</label>
          </div>
          <div class="right">
            <button class="button button-edit" @click="openEditModal(item)">Edit</button>
            <button @click="handleDelete(item)" class="button button-delete">Delete</button>
          </div>
        </li>
      </ul>

      <footer class="footer">
        <p>Công việc hoàn thành:</p>
        <p>
          <b>{{completeJobs}}</b> /
          <b>{{listJob.length}}</b>
        </p>
      </footer>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, watch, watchEffect } from "vue";
const inputValue = ref("");
const listJob = reactive(JSON.parse(localStorage.getItem("jobs")) || []);
const completeJobs = ref(0);
const showEditModal = ref(false);
const editJob = ref({ id: null, name: "" });
/**
 * Hàm lưu trữ dữ liệu trên localStorage
 * @param key key của dữ liệu
 * @param data là mảng công việc
 */
const savaData = (key, data) => {
  localStorage.setItem(key, JSON.stringify(data));
};
// Hàm thêm công việc
const handleAddJob = () => {
  // Kiểm tra xem ô nhập liệu có trống hay không
  if (!inputValue.value) {
    alert("Tên công việc không được để trống.");
    return;
  }

  // Kiểm tra xem tên công việc có bị trùng hay không
  const findJobByName = listJob.find(item => item.name === inputValue.value);
  if (findJobByName) {
    alert(`Tên công việc '${inputValue.value}' đã tồn tại.`);
    return;
  }

  // Thêm công việc mới vào danh sách
  listJob.push({
    id: Math.ceil(Math.random() * 100000), // Tạo id ngẫu nhiên cho công việc
    name: inputValue.value, // Lấy tên công việc từ ô nhập liệu
    status: false // Trạng thái công việc mặc định là chưa hoàn thành
  });

  // Lưu danh sách công việc vào localStorage dưới dạng chuỗi JSON
  savaData("jobs", listJob);
  // Sau khi thêm, reset lại ô nhập liệu về trống
  inputValue.value = "";
};
/**
 * Hàm cập nhật trạng thái công việc
 * @param id Id của công việc cần cập nhật
 */
const handleUpdateStatus = id => {
  // Tìm kiếm vị trí của công vc trong mảng
  const findIndexJob = listJob.findIndex(item => item.id === id);
  // Cập nhật thông tin công việc theo vị trí
  listJob[findIndexJob].status = !listJob[findIndexJob].status;
  // lưu dữ liệu lên localstorage
  savaData("jobs", listJob);
};
/**
 * Hàm xóa thông tin 1 công việc
 * @param item Đối tượng cộng việc cần xóa
 */
const handleDelete = item => {
  const isConfirmDelete = confirm(
    `Bạn có muốn xóa công việc "${item.name}" ko ??`
  );
  if (isConfirmDelete) {
    // Tiến hành xóa
    // B1 : Lọc ra những bản ghi có id khác với id cần xóa
    const filterJobs = listJob.filter(jobItem => jobItem.id !== item.id);
    // Cập nhật lại dữ liệu cho listJob
    listJob.length = 0; //Làm rỗng mảng cũ
    listJob.push(...filterJobs); //push dữ liệu mới vào trong mảng
    // lưu dữ liệu trên localStorage
    savaData("jobs", listJob);
  }
};
// Sửa công việc
const openEditModal = item => {
  editJob.value = { ...item };
  showEditModal.value = true;
};

const handleSaveEdit = () => {
  const findIndexJob = listJob.findIndex(job => job.id === editJob.value.id);
  listJob[findIndexJob].name = editJob.value.name;
  savaData("jobs", listJob);
  showEditModal.value = false;
};

const closeModal = () => {
  showEditModal.value = false;
};

const updateStatusJob = () => {
  // Lọc ra những công việc có status = true
  const filterJobComplete = listJob.filter(item => item.status);
  // Cập nhật lại giá trị cho biến completeJobs
  completeJobs.value = filterJobComplete.length;
};
// Trong vue thì use watch để lắng nghe sự thay đổi của 1 biến
// watch(
//   listJob,
//   () => {
//     updateStatusJob();
//   },
//   {
//     deep: true,
//     immediate: true
//   }
// );

watchEffect(() => {
  updateStatusJob();
});
</script>

<style scoped>
.container {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.heading {
  text-align: center;
  font-size: 24px;
  padding-bottom: 24px;
}

.todo {
  width: 600px;
  border: 1px solid #dadada;
  padding: 20px 24px;
  border-radius: 8px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
}

.header {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
  gap: 12px;
}

.input {
  height: 36px;
  border: 1px solid #dadada;
  outline: none;
  border-radius: 4px;
  box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  flex: 1;
  padding: 0 16px;
}

.button {
  height: 36px;
  border: 1px solid transparent;
  color: #fff;
  outline: none;
  border-radius: 4px;
  padding: 0 16px;
  cursor: pointer;
}

.button-add {
  background-color: blue;
}
.right {
  display: flex;
  gap: 20px;
}
.button-delete {
  background-color: red;
}
.button-edit {
  background-color: orange;
}

.list-item {
  display: flex;
  flex-direction: column;
  gap: 20px;
  margin-bottom: 20px;
}

.item {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

input[type="checkbox"] {
  height: 18px;
  width: 18px;
}

.left {
  display: flex;
  align-items: center;
  gap: 8px;
}

.footer {
  display: flex;
  gap: 8px;
}

/* CSS cho modal */
.custom-modal {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.4); /* Màu nền tối mờ */
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  width: 400px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  position: relative;
}
.close_save {
  width: 390px;
  display: flex;
  justify-content: space-between;
}
.modalBtn {
  display: flex;
  gap: 20px;
}
.close {
  position: absolute;
  top: 10px;
  right: 20px;
  color: #aaa;
  font-size: 24px;
  cursor: pointer;
}

.close:hover {
  color: #000;
}

.modal-content h2 {
  margin-bottom: 20px;
}

.modal-content .input {
  width: 340px;
  margin-bottom: 20px;
}

.modal-content .button {
  background-color: green;
}
.but {
  background-color: grey;
  border: none;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
}
</style>
