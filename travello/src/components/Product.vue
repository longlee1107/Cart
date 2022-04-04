<template>
<div class="content-box">
    <div class="name"><strong>Name: </strong>{{product.name}}</div>
    <div class="price"><strong>Price: </strong>{{product.price}}</div>
    <div class="brand"><strong>Brand: </strong>{{product.brand}}</div>
    <div class="description"><strong>Decription: </strong>{{product.description}}</div>
    <div class="color"><strong>Color: </strong>
        <div class="color-inner" v-for="color in product.color" :key="color.code">
            <a href="color.code">{{color.name}}({{color.number}})</a>
        </div>
    </div>
    <div class="add-to-cart">
        <button @click="addToCart()">ADD</button>
    </div>
</div>
</template>

<script>
export default {
    props: {
        product: {
            type: Object,
            required: true
        },
        color: {
            type: Array,
            required: true
        }
    },
    data() {
        return {

        }
    },
    methods: {
        addToCart() {
            this.$emit('addToCart', this.product)
        },
    },
}
</script>

<style>
.color {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-start;
    margin: 5px;
}

.color .color-inner a {
    margin-left: 5px;
    text-decoration: none;
    color: #000;
}
.color .color-inner a:hover {
    color: #00b894;
}
</style>
