<template>
  <div>
    <form
      style="width: 300px; display: flex; flex-direction: column; gap: 5px"
      @submit.prevent="handleSubmit"
    >
      <h1 style="text-align: center">Đăng nhập tài khoản</h1>

      <label for="">Email</label>
      <input type="text" v-model="user.email" />
      <span v-if="errors.email" style="color: red">{{ errors.email }}</span>

      <label for="">Mật khẩu</label>
      <input type="password" v-model="user.password" />
      <span v-if="errors.password" style="color: red">{{
        errors.password
      }}</span>

      <button
        style="
          padding: 10px;
          background-color: blue;
          color: white;
          border: none;
        "
      >
        Đăng nhập
      </button>

      <p v-if="loginMessage" :style="{ color: loginSuccess ? 'green' : 'red' }">
        {{ loginMessage }}
      </p>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";

const user = ref({
  email: "",
  password: "",
});

const errors = ref({
  email: "",
  password: "",
});

const loginMessage = ref("");
const loginSuccess = ref(false);

// Kiểm tra validate dữ liệu
const validateForm = () => {
  errors.value = { email: "", password: "" };

  if (!user.value.email) {
    errors.value.email = "Email không được để trống";
  }

  if (!user.value.password) {
    errors.value.password = "Mật khẩu không được để trống";
  }

  // Kiểm tra nếu có lỗi nào thì trả về false
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
    const storedUser = JSON.parse(localStorage.getItem("user"));

    if (
      storedUser &&
      storedUser.email === user.value.email &&
      storedUser.password === user.value.password
    ) {
      loginMessage.value = "Đăng nhập thành công";
      loginSuccess.value = true;
    } else {
      loginMessage.value = "Đăng nhập thất bại";
      loginSuccess.value = false;
    }
  }
};
</script>

<style></style>
