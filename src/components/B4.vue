<template>
  <div style="width: 300px; display: flex; flex-direction: column">
    <label for="">Tiến độ hoành thành: {{ complete }} %</label>
    <input type="range" v-model="complete" @change="handleChange" />
  </div>
</template>

<script setup>
import { ref } from "vue";
const complete = ref(0);
const handleChange = (e) => {
  complete.value = e.target.value;
};
</script>

<style></style>
