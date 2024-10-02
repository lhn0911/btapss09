<template>
  <div style="width: 300px; display: flex; flex-direction: column">
    <label for="">Email</label>
    <input type="text" v-model="email" @change="handleChange" />
    <p>giá trị: {{ inputValue }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";
const email = ref("");
const handleChange = (e) => {
  email.value = e.target.value;
};
</script>

<style></style>
