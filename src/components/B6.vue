<template>
  <div style="width: 500px">
    <label>Hoppy: {{ hoppy }}</label> <br />
    <input type="checkbox" value="Đá bóng" v-model="hoppy" />Đá bóng <br />
    <input type="checkbox" value="Bóng chuyền" v-model="hoppy" />Bóng chuyền
    <br />
    <input type="checkbox" value="Code" v-model="hoppy" />Code <br />
    <input type="checkbox" value="Bơi lội" v-model="hoppy" />Bơi lội <br />
  </div>
</template>

<script setup>
import { ref } from "vue";
const hoppy = ref([]);
</script>

<style></style>
