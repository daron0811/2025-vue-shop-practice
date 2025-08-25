## 環境安裝

```bash
# 1) 建立空白 Vue 3（Vite）專案
npm create vue@latest 2025-vue-shop-practice
cd 2025-vue-shop-practice
npm install

# 2) 安裝 Bootstrap 與 Popper（專案實際有用到）
npm i bootstrap

# 3) 開發
npm run dev
```

> **Bootstrap 實際匯入位置**：`src/main.js`

```js
// src/main.js
import './assets/main.css'
import 'bootstrap'                              
import 'bootstrap/dist/css/bootstrap.min.css'   

import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

---

## 專案資料夾結構

```
src/
├─ assets/
│  └─ main.css
├─ components/
│  ├─ AlertBox.vue          # 通知視窗
│  ├─ CartList.vue          # 購物車清單
│  └─ ProductList.vue       # 產品清單
├─ datas/
│  └─ ProductItems.js       # 資料庫
├─ App.vue                  # 主流程
├─ Ref.vue                  # 版型參考（非主流程）
└─ main.js
```

---

## 整體流程（依實作）

1. `datas/ProductItems.js` 匯出 `productDatas` 商品資料供頁面使用。
2. `App.vue` 匯入並以 `ProductList` 顯示商品，透過 `emit_addToCart` 把選取商品傳回父層。
3. `App.vue` 在父層接到商品後，檢查購物車中是否已有相同 `id`：
   - 有 → `quantity += 1`，並在 `AlertBox` 顯示「已有重複品項…」。
   - 無 → 使用展開運算子 `...product` 新增至購物車，並顯示「新增商品…」。
4. `CartList.vue` 以 `v-for` 呈現購物車清單，並觸發 `emit_cart_delete` 移除項目。
5. `App.vue` 以 `computed` 計算總價 `cartPriceTotal`，於畫面顯示。
6. 介面排版完全使用 Bootstrap（Grid、Card、List Group、Button、Utilities）。

---

## Vue 3：專案中實際使用的語法

> 官方文件：[https://vuejs.org/](https://vuejs.org/)

### 1) `defineProps` / `defineEmits`

- **出處**：`components/ProductList.vue`, `components/CartList.vue`

```vue
<!-- components/ProductList.vue -->
<script setup>
const props = defineProps({
  prop_products: { type: Object, require: true }
})

const emit = defineEmits(['emit_addToCart'])

const addToCart = (product) => {
  emit('emit_addToCart', product)
}
</script>
```

```vue
<!-- components/CartList.vue -->
<script setup>
const props = defineProps({
  prop_carts: { type: Object, require: true }
})

const emit = defineEmits(['emit_cart_delete'])

const removeFromCart = (cartItem) => {
  emit('emit_cart_delete', cartItem)
}
</script>
```

### 2) 模板指令：`v-for`、`:key`、事件、插值

- **出處**：`components/ProductList.vue`

```html
<div class="col-md-4 mb-4" v-for="product in prop_products" :key="product.id">
  <div class="card h-100">
    <img :src="product.img" class="card-img-top">
    <div class="card-body">
      <h5 class="card-title">{{ product.name }}</h5>
      <p class="card-text">{{ product.description }}</p>
      <p class="fw-bold text-primary">$ {{ product.price }}</p>
      <button class="btn btn-success w-100" v-on:click="addToCart(product)">加入購物車</button>
    </div>
  </div>
</div>
```

- **出處**：`components/CartList.vue`（注意：使用 `:key="cartItem.cartId"`）

```html
<li v-for="cartItem in prop_carts" :key="cartItem.cartId"
    class="list-group-item d-flex justify-content-between align-items-center">
  ...
</li>
```

### 3) `ref` / `computed` 與陣列運算

- **出處**：`App.vue`（計算總價）

```js
import { ref, computed } from 'vue'

const cart = ref([])

const cartPriceTotal = computed(() => {
  return cart.value.reduce((pre, next) => pre + next.price * next.quantity, 0)
})
```

### 4) 物件展開運算子（JS）

- **出處**：`App.vue`（加入新項目）

```js
cart.value.push({
  ...product,
  id: product.id,
  quantity: 1,
})
```

### 5) `watch` 與 `v-html`

- **出處**：`components/AlertBox.vue`

```html
<!-- 以 v-if 控制顯示，訊息以 v-html 插入（已在專案中使用） -->
<div class="toast show align-items-center text-white bg-success border-0" v-if="msg">
  <div class="d-flex">
    <div class="toast-body"><span v-html="msg"></span></div>
    <button type="button" class="btn-close btn-close-white me-2 m-auto" @click="msg = ''"></button>
  </div>
</div>
```

```js
import { watch } from 'vue'

// 專案中監看 warnMsg，並於 3 秒後自動清除
if (warnMsg) {
  watch(warnMsg, (newVal) => {
    if (newVal) {
      setTimeout(() => { warnMsg.value = '' }, 3000)
    }
  })
}
```

> 備註：`AlertBox.vue` 採 **純模板 Toast 樣式**（無使用 Bootstrap 的 JS Toast API）。

---

## Bootstrap：專案中實際使用的語法

> 官方文件：[https://getbootstrap.com/](https://getbootstrap.com/)

### 1) 全域載入（CSS + JS）

- **出處**：`src/main.js`

```js
import 'bootstrap'                              // JS Bundle（含 Popper）
import 'bootstrap/dist/css/bootstrap.min.css'   // 樣式
```

### 2) Grid 與排版 Utilities

- **出處**：`App.vue`, `Ref.vue`

```html
<div class="container py-4">
  <div class="row">
    <div class="col-md-8">...</div>
    <div class="col-md-4">...</div>
  </div>
</div>

<!-- 同一區塊左右各一 -->
<div class="d-flex justify-content-between mb-3"> ... </div>
```

### 3) Card 元件

- **出處**：`components/ProductList.vue`, `Ref.vue`

```html
<div class="card h-100">
  <img :src="product.img" class="card-img-top">
  <div class="card-body">
    <h5 class="card-title">{{ product.name }}</h5>
    <p class="card-text">{{ product.description }}</p>
    <p class="fw-bold text-primary">$ {{ product.price }}</p>
    <button class="btn btn-success w-100">加入購物車</button>
  </div>
</div>
```

### 4) List Group + 按鈕樣式

- **出處**：`components/CartList.vue`

```html
<ul class="list-group mb-3" v-if="prop.prop_carts.length != 0">
  <li class="list-group-item d-flex justify-content-between align-items-center"> ...
    <button class="btn btn-sm btn-outline-danger ms-2">移除</button>
  </li>
</ul>
```

### 5) Toast 樣式（純樣式顯示）

- **出處**：`components/AlertBox.vue`, `Ref.vue`

```html
<div class="toast show align-items-center text-white bg-success border-0">
  <div class="d-flex">
    <div class="toast-body">這是通知訊息</div>
    <button type="button" class="btn-close btn-close-white me-2 m-auto"></button>
  </div>
</div>
```

> 專案採用 **Bootstrap 樣式** 與 Vue 控制邏輯（`v-if` / `watch`），**未**建立 `new bootstrap.Toast(...)` JS 實例。

---

## 參考：資料載入

- **出處**：`datas/ProductItems.js`

```js
export const productDatas = [
  { id: 0, name: '耳罩式藍牙耳機', description: '舒適配戴，支援降噪技術', price: 2490, img: '...'},
  ...
]
```

- **使用方式**（示意）：在 `App.vue` 匯入後傳給 `ProductList`。

---

## 其他筆記
 **vue src的用法**
```js
// components\ProductList.vue
<img :src=product.img class="card-img-top"> <!--留意vue的src用法-->
```

 **inject、provide的用法**
```js
// App.vue
import { ref, computed, provide } from 'vue';
const alertMsg = ref("");
const alertWarnMsg = ref("");
provide('showAlert', alertMsg); // 定義顯示訊息通知的Key及訊息
provide('showWarnAlert', alertWarnMsg);

// components\AlertBox.vue
import { inject, watch } from 'vue'

// 定義inject的方法，可以變數或函式功能
const msg = inject('showAlert', '') // 第二個參數是沒有帶入參數時的預設值
const warnMsg = inject('showWarnAlert', '')

```


## 小結

- Vue 3（本專案實際使用）：`defineProps`, `defineEmits`, `ref`, `computed`, `watch`、模板指令（`v-for`、`:key`、事件、插值）、以及 **展開運算子（JS）**。

- Bootstrap（本專案實際使用）：全域載入、Grid、Card、List Group、Buttons、Utilities（`d-flex`, `justify-content-between`, 間距類）。


