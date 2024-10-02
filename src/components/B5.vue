<template>
  <div style="width: 300px">
    <label>Giới tính: {{ gender }}</label> <br />
    <input type="radio" value="Nam" v-model="gender" />Nam <br />
    <input type="radio" value="Nữ" v-model="gender" />Nữ <br />
    <input type="radio" value="Khác" v-model="gender" />Khác
  </div>
</template>

<script setup>
import { ref } from "vue";
const gender = ref("Nam");
</script>

<style></style>
