<template>
  <div>
    <form
      action=""
      style="width: 300px; display: flex; flex-direction: column; gap: 5px"
      @submit.prevent="handleSubmit"
    >
      <h1 style="text-align: center">Thêm mới sản phẩm</h1>
      <label for="">Mã sản phẩm</label>
      <input type="text" v-model="product.productCode" />
      <label for="">Tên sản phẩm</label>
      <input type="text" v-model="product.productName" />
      <label for="">Giá</label>
      <input type="text" v-model="product.price" />
      <label for="">Số lượng</label>
      <input type="number" v-model="product.quantity" />
      <button
        style="
          padding: 10px;
          background-color: blue;
          color: white;
          border: none;
        "
      >
        Thêm mới
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";
const product = ref({
  productCode: "",
  productName: "",
  price: 0,
  quantity: 0,
});

const handleSubmit = () => {
  console.log(product.value);
};
</script>

<style></style>
