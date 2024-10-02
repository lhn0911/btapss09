<template>
  <div>
    <form
      style="width: 300px; display: flex; flex-direction: column; gap: 5px"
      @submit.prevent="handleSubmit"
    >
      <h1 style="text-align: center">Đăng ký tài khoản</h1>

      <label for="">Tên sinh viên</label>
      <input type="text" v-model="user.userName" ref="userNameInput" />
      <span v-if="errors.userName" style="color: red">{{
        errors.userName
      }}</span>

      <label for="">Email</label>
      <input type="text" v-model="user.email" />
      <span v-if="errors.email" style="color: red">{{ errors.email }}</span>

      <label for="">Mật khẩu</label>
      <input type="password" v-model="user.password" />
      <span v-if="errors.password" style="color: red">{{
        errors.password
      }}</span>

      <label for="">Số điện thoại</label>
      <input type="text" v-model="user.phone" />

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
  phone: "",
});

const errors = ref({
  userName: "",
  email: "",
  password: "",
});
const userNameInput = ref(null);

const validateForm = () => {
  errors.value = { userName: "", email: "", password: "" };

  if (!user.value.userName) {
    errors.value.userName = "Tên sinh viên không được để trống";
  }

  if (!user.value.email) {
    errors.value.email = "Email không được để trống";
  } else if (localStorage.getItem(user.value.email)) {
    errors.value.email = "Email đã tồn tại";
  }

  if (!user.value.password) {
    errors.value.password = "Mật khẩu không được để trống";
  }

  for (let key in errors.value) {
    if (errors.value[key]) {
      return false;
    }
  }

  return true;
};

// Xử lý khi submit
const handleSubmit = () => {
  if (validateForm()) {
    localStorage.setItem("user", JSON.stringify(user.value));
    user.value = {
      userName: "",
      email: "",
      password: "",
      phone: "",
    };
    userNameInput.value.focus();
  }
};
</script>

<style></style>
