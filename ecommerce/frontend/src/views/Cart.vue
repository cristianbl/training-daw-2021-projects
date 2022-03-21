<template>
    <div>

        <h1>Carrito</h1>
        
        <Carrito
        v-for="orderProduct in cart"
        :key="orderProduct.id"
        :item='orderProduct.item'
        :quantity='orderProduct.quantity'
        >
        </Carrito> 
        <h1> </h1>
    </div>
</template>

<script>

import Carrito from '../components/Carrito.vue'

export default {
    name:'Cart',
    components:{
        Carrito
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