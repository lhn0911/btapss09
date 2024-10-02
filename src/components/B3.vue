<template>
  <div style="width: 300px; display: flex; flex-direction: column">
    <label for="">Ngày Sinh: {{ dayOfBirth }}</label>
    <input type="date" v-model="dayOfBirth" @change="handleChange" />
  </div>
</template>

<script setup>
import { ref } from "vue";
const dayOfBirth = ref("");
const handleChange = (e) => {
  dayOfBirth.value = e.target.value;
};
</script>

<style></style>
