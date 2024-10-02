<template>
  <div style="width: 500px">
    <label>Sở thích: {{ interests }}</label> <br />
    <input type="checkbox" value="Đá bóng" v-model="interests" />Đá bóng <br />
    <input type="checkbox" value="Bóng chuyền" v-model="interests" />Bóng chuyền
    <br />
    <input type="checkbox" value="Code" v-model="interests" />Code <br />
    <input type="checkbox" value="Bơi lội" v-model="interests" />Bơi lội <br />
  </div>
</template>

<script setup>
import { ref } from "vue";
const interests = ref([]);
</script>

<style></style>
