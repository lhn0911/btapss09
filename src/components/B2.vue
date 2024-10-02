<template>
  <div style="width: 300px; display: flex; flex-direction: column">
    <label for="">Màu sắc</label>
    <input type="color" v-model="color" />
  </div>
</template>

<script setup>
import { ref } from "vue";
const color = ref("#000000");
</script>

<style></style>
