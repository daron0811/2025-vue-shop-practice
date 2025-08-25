<template>
    <div class="row">
        <div class="col-md-4 mb-4" v-for="product in prop_products" :key="product.id">
            <div class="card h-100">
                <img :src=product.img class="card-img-top"> <!--留意vue的src用法-->
                <div class="card-body">
                    <h5 class="card-title">{{ product.name }}</h5>
                    <p class="card-text">{{ product.description }}</p>
                    <p class="fw-bold text-primary">$ {{ product.price }}</p>
                    <button class="btn btn-success w-100" v-on:click="addToCart(product)"> 加入購物車 </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

const props = defineProps({
    prop_products: { type: Object, require: true }
})

const emit = defineEmits(['emit_addToCart'])

//新增購物車項目
const addToCart = (product) => {
    emit('emit_addToCart', product);
}

</script>