<template>
    <div>
        <h1>Carrito</h1>
        <Cart
        v-for="orderProduct in cart"
        :key="orderProduct.id"
        :item='orderProduct.item'
        :quantity='orderProduct.quantity'
        >
        </Cart>
        <h1> </h1>
    </div>
</template>

<script>


export default {
    name:'Cart',
    components:{
        Cart
    },
    data(){
        return {
            cart:[]
        }
    },
    methods:{

    },
    created(){
        fetch('http://localhost:3000/cart')
        .then(result => result.json())
        .then(data => {
            this.cart = data
            })
    },
    computed:{

    }

}
</script>

<style>

</style>