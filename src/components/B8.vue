<template>
  <div>
    <form
      action=""
      style="width: 300px; display: flex; flex-direction: column; gap: 5px"
      @submit.prevent="handleSubmit"
    >
      <h1 style="text-align: center">Thêm mới tài khoản</h1>
      <label for="">Họ và tên</label>
      <input type="text" v-model="user.userName" />
      <label for="">Email</label>
      <input type="text" v-model="user.email" />
      <label for="">Mật khẩu</label>
      <input type="password" v-model="user.password" />
      <label for="">Nhập lại mật khẩu</label>
      <input type="password" v-model="user.rePassword" />
      <button
        style="
          padding: 10px;
          background-color: blue;
          color: white;
          border: none;
        "
      >
        Đăng ký
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
const user = ref({
  userName: "",
  email: "",
  password: "",
  rePassword: "",
});

const handleSubmit = () => {
  console.log(user.value);
};
</script>

<style></style>
