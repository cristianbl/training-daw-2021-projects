<template>
  <div>

    <ProductDetailComponent
    :item='item'>

    </ProductDetailComponent>
    
  </div>
</template>

<script>
// @ is an alias to /src
import ProductDetailComponent from '@/components/ProductDetailComponent.vue'

export default {

    name: "ProductDetail",
    components:{
        ProductDetailComponent
    },

    data(){
        
        console.log(url)

        return {
            item:{}
        }
    },
    created(){
        let url = `http://localhost:3000/products/${this.$router.params.id}`;
        console.log(url)
        fetch(this.url)
        .then(json=> json.json())
        .then(data=> this.item = data)
    },
    props: {
   
    },
  
    methods: {
   
    },
    computed:{
       id(){
           return this.$router.params.id
       }
    }
  };
</script>
