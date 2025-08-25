<!--版型參考用 : 來源 :https://codepen.io/hexschool/pen/EaVwgmK-->

<template>
  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 ProductList -->
      <div class="col-md-8">
        <h2 class="mb-3">商品列表</h2>
        <div class="row">

          <div class="col-md-4 mb-4">
            <div class="card h-100">
              <img
                src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                class="card-img-top">
              <div class="card-body">
                <h5 class="card-title">耳罩式藍牙耳機</h5>
                <p class="card-text">舒適配戴，支援降噪技術</p>
                <p class="fw-bold text-primary">$ 2490</p>
                <button class="btn btn-success w-100"> 加入購物車 </button>
              </div>
            </div>
          </div>

          <div class="col-md-4 mb-4">
            <div class="card h-100">
              <img
                src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                class="card-img-top">
              <div class="card-body">
                <h5 class="card-title">耳罩式藍牙耳機</h5>
                <p class="card-text">舒適配戴，支援降噪技術</p>
                <p class="fw-bold text-primary">$ 2490</p>
                <button class="btn btn-success w-100"> 加入購物車 </button>
              </div>
            </div>
          </div>

          <div class="col-md-4 mb-4">
            <div class="card h-100">
              <img
                src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                class="card-img-top">
              <div class="card-body">
                <h5 class="card-title">耳罩式藍牙耳機</h5>
                <p class="card-text">舒適配戴，支援降噪技術</p>
                <p class="fw-bold text-primary">$ 2490</p>
                <button class="btn btn-success w-100"> 加入購物車 </button>
              </div>
            </div>
          </div>

          <div class="col-md-4 mb-4">
            <div class="card h-100">
              <img
                src="https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&amp;w=2065&amp;auto=format&amp;fit=crop&amp;ixlib=rb-4.1.0&amp;ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
                class="card-img-top">
              <div class="card-body">
                <h5 class="card-title">耳罩式藍牙耳機</h5>
                <p class="card-text">舒適配戴，支援降噪技術</p>
                <p class="fw-bold text-primary">$ 2490</p>
                <button class="btn btn-success w-100"> 加入購物車 </button>
              </div>
            </div>
          </div>

        </div>
      </div>

      <!-- 購物車區 CartList -->
      <div class="col-md-4">
        <h2 class="mb-3">購物車</h2>
        <ul class="list-group mb-3">

          <li class="list-group-item d-flex justify-content-between align-items-center">
            <div>
              <h6 class="my-0">時尚藍牙耳機</h6>
              <small class="text-muted">數量：1</small>
            </div>
            <div>
              <span class="text-muted">$7990</span>
              <button class="btn btn-sm btn-outline-danger ms-2"> 移除 </button>
            </div>
          </li>

          <li class="list-group-item d-flex justify-content-between align-items-center">

            <div>
              <h6 class="my-0">時尚藍牙耳機</h6>
              <small class="text-muted">數量：1</small>
            </div>
            <div>
              <span class="text-muted">$7990</span>
              <button class="btn btn-sm btn-outline-danger ms-2"> 移除 </button>
            </div>
          </li>



        </ul>

        <!--額外新增項目-->
        <div class="text-end mb-3">
          <h5>總計: <span>${{ sum }}</span></h5>
        </div>

      </div>
    </div>

    <!-- 通知元件 AlertBox -->
    <div class="position-fixed top-0 end-0 p-3" style="z-index: 1050">

      <div class="toast show align-items-center text-white bg-success border-0">
        <div class="d-flex">
          <div class="toast-body">這是通知訊息</div>
          <button type="button" class="btn-close btn-close-white me-2 m-auto"></button>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
</script>

<style></style>