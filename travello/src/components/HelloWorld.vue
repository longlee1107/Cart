<template>
<div class="wrapper">
    <div class="cart">
        <button @click="showModal = !showModal">Show</button>
        <ul v-if="!showModal">
            <li class="list-of-buy" v-for="product in ListToPurchase" :key="product.id">
                <div class="product">
                    <div class="image-inner"><img :src="product.thumb" alt=""></div>
                    <div class="name">{{product.name}}</div>
                    <div class="price">{{product.price}}</div>
                    <div class="brand">{{product.brand}}</div>
                    <div class="description">{{product.description}}</div>
                    <div class="count">{{product.count}}</div>
                    <div class="remove-to-cart">
                        <button @click="removeToCart(product)">Remove</button>
                    </div>
                </div>
            </li>
            <div class="total">Total: {{total}}</div> 
        </ul>
        <div class="product" v-for="product in List" :key="product.id">
            <div class="image-inner">
                <img :src="product.thumb" alt="">
            </div>
            <Product :color="color" :product="product" @addToCart="addToCart" />
            <div v-if="product.hot">Best Seller</div>
            <div v-else>Not Best Seller</div>
        </div>
    </div>
</div>
</template>

<script>
import Product from "./Product.vue"
export default {
    name: "HelloWorld",
    data() {
        return {
            showModal: false,
            ListToBuy: [],
            ListToPurchase: [],
            total: 0,
            List: [{
                thumb: "http://placeimg.com/640/480",
                name: "Fantastic Fresh Hat",
                description: "Carbonite web goalkeeper gloves are ergonomically designed to give easy fit",
                price: 151,
                id: 1,
                hot: false,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0
            }, {
                thumb: "http://placeimg.com/640/480",
                name: "Gorgeous Fresh Bike",
                description: "The Nagasaki Lander is the trademarked name of several series of Nagasaki sport bikes, that started with the 1984 ABC800J",
                price: 288,
                id: 2,
                hot: true,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0
            }, {
                thumb: "http://placeimg.com/640/480",
                name: "Intelligent Wooden Shirt",
                description: "The automobile layout consists of a front-engine design, with transaxle-type transmissions mounted at the rear of the engine and four wheel drive",
                price: 343,
                id: 3,
                hot: true,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0
            }, {
                thumb: "http://placeimg.com/640/480",
                name: "Intelligent Plastic Salad",
                description: "New range of formal shirts are designed keeping you in mind. With fits and styling that will make you stand apart",
                price: "753.00",
                id: 4,
                hot: true,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0
            }, {
                thumb: "http://placeimg.com/640/480",
                name: "Rustic Steel Bike",
                description: "The beautiful range of Apple Naturalé that has an exciting mix of natural ingredients. With the Goodness of 100% Natural Ingredients",
                price: 988,
                id: 5,
                hot: false,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0

            }, {
                thumb: "http://placeimg.com/640/480",
                name: "Awesome Steel Ball",
                description: "The automobile layout consists of a front-engine design, with transaxle-type transmissions mounted at the rear of the engine and four wheel drive",
                price: 642,
                id: 6,
                hot: true,
                brand: "Nike",
                release: "2018-01-01",
                color: [{
                        name: "Black",
                        code: "#000000",
                        number: 2
                    },
                    {
                        name: "White",
                        code: "#ffffff",
                        number: 4
                    }
                ],
                count: 0
            }, ]

        };
    },
    methods: {
        addToCart(item) {
            this.ListToBuy.push(item),

                this.ListToPurchase = this.ListToBuy.filter((data, index, self) => {
                    return self.findIndex(t => t.id === data.id) === index;
                });
            this.ListToPurchase.forEach(item => {
                item.count = this.ListToBuy.filter(data => data.id === item.id).length;
            });
            this.total = this.ListToPurchase.reduce((total, item) => {
                return total + item.price * item.count;
            }, 0);
        },
        removeToCart(data) {
            this.ListToPurchase.splice(this.ListToPurchase.indexOf(data), 1);
            this.$emit('removeToCart', this.article);
        }

    },
    components: {
        Product
    }
}
</script>

<style>
.wrapper .product {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 2rem;
    border: #00b894 1px solid;
    margin: 5px;
    padding: 5px;
}

.wrapper .product .image-inner,
.list-to-buy .product .image-inner {
    width: 300px;
    height: 300px;
    overflow: hidden;
    margin: 1rem 0;
}

.wrapper .product .image-inner img,
.list-to-buy .product .image-inner img {
    object-fit: cover;
    width: 100%;
    height: 100%;
}

li {
    list-style: none;
}

.wrapper .product .content-box {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    width: 60%;
    padding-right: 20%;
}

.wrapper .product .add-to-cart {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 20%;
}

.wrapper .product .add-to-cart button {
    background-color: #00b894;
    color: #fff;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    width: 120px;
    height: 80px;
}

ul {
    list-style: none;
    border: #00b894 1px solid;
}
.total{
  display: flex;
  justify-content: space-between;
}
</style>
