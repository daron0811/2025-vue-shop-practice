<template>
  <div id="app" class="container py-4">
    <div class="row">

      <!-- 商品列表區 ProductList -->
      <div class="col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <ProductList :prop_products="products" @emit_addToCart="addToCart" />
      </div>

      <!-- 購物車區 CartList -->
      <div class="col-md-4">
        <h2 class="mb-3">購物車</h2>
        <CartList :prop_carts="cart" @emit_cart_delete="removeFormCart" />
        <!--額外新增項目-->
        <div class="d-flex justify-content-between mb-3">
          <h6 class="text-end mb-3">總計 : <span>$ {{ cartPriceTotal }}</span></h6>
        </div>
      </div>
      
    </div>

    <!-- 通知元件 AlertBox -->
    <div class="position-fixed top-0 end-0 p-3 m" style="z-index: 1050">
      <alert-box />
    </div>

  </div>
</template>

<script setup>

import { ref, computed, provide } from 'vue';
import ProductList from './components/ProductList.vue';     //商品列表
import CartList from './components/CartList.vue';           //購物車
import AlertBox from './components/AlertBox.vue';           //訊息通知
import { productDatas } from './datas/ProductItems.js'      //商品資料來源

const products = ref(productDatas);   //儲存商品用
const cart = ref([                    //儲存購物車用
  // { id, title, price, quantity, ... }
]);

const alertMsg = ref("");
const alertWarnMsg = ref("");
provide('showAlert', alertMsg); // 定義顯示訊息通知的Key及訊息
provide('showWarnAlert', alertWarnMsg);


// 購物車邏輯

//加入購物車
const addToCart = (product) => {
  const existItem = cart.value.find(item => item.id === product.id);

  if (existItem) {
    alertMsg.value = `已有重複品項 , 新增 1 筆數量至 <span style="color: yellow; font-weight: bold;">${product.name}</span>`
    existItem.quantity += 1;
  }
  else {
    cart.value.push(
      {
        ...product,///展開運算子，攤開物件內容
        id: product.id,
        quantity: 1,
        //timeStamp: new Date().getTime(),  //用時間戳記作為購物車內追蹤
      }
    );
    alertMsg.value = `新增商品 <span style="color: yellow; font-weight: bold;">${product.name}</span> 至購物車`
  }

}

//刪除購物車商品
const removeFormCart = (cartItem) => {
  cart.value = cart.value.filter((item) => cartItem.id !== item.id);
  alertMsg.value = `至購物車刪除商品 <span style="color: yellow; font-weight: bold;">${cartItem.name}</span> `
}

//計算購物車目前總價
const cartPriceTotal = computed(() => {
  return cart.value.reduce((pre, next) => {
    return pre + next.price * next.quantity;
  }, 0);
});


</script>


<style scoped></style>
