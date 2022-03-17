<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <div class = "card" style="display: flex; flex-wrap:wrap; justify-content: center; gap:12px" >
        <ProductCard
        v-for="item in items"
        :key = "item.id"
        :item="item" style="width:26%;  border: 1px solid black">
        </ProductCard>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import ProductCard from "../components/ProductCard.vue"
export default {
  name: 'Home',
  components: {
    ProductCard
  },
  created() {
      fetch('http://localhost:3000/products')
        .then(result => result.json())
        .then(data => this.items = data)
    },
    data(){
      return {
        items: []
      }
    }

}
</script>
