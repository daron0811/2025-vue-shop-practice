<template>
    <ul class="list-group mb-3" v-if="prop.prop_carts.length != 0">

        <li v-for="cartItem in prop_carts" :key="cartItem.cartId"
            class="list-group-item d-flex justify-content-between align-items-center">
            <div>
                <h6 class="my-0">{{ cartItem.name }}</h6>
                <small class="text-muted">數量：{{ cartItem.quantity }}</small>
            </div>
            <div>
                <span class="text-muted">${{ itemSubtotal(cartItem) }}</span>
                <button class="btn btn-sm btn-outline-danger ms-2" @click="removeFromCart(cartItem)"> 移除
                </button>
            </div>
        </li>
    </ul>
    <div class="alert alert-primary" v-else-if="prop.prop_carts.length == 0">
        尚未選擇商品
    </div>

</template>

<script setup>
const prop = defineProps({
    prop_carts: { type: Object, require: true }
})

const emit = defineEmits(['emit_cart_delete']);

//移除購物車項目
const removeFromCart = (cartItem) => {
    emit('emit_cart_delete', cartItem);
}

//計算購物車該商品價格
const itemSubtotal = (cartItem) => {
    return cartItem.price * cartItem.quantity;
};
</script>