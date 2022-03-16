<template>
    <div>
    <h4>{{item.name}}</h4>
    <img class="img" :src="item.mainImage" />
      <h5 class="price"> Price: ${{item.price}}</h5>
      <p class="description">Description: {{item.description}} </p>
      <router-link :to="{name: 'ProductDetail', params: {id: item.id}}">
        <button>Ver</button>
      </router-link>
    </div>
</template>

<script>

export default {
    props: ['item'],
  components: {

  },
  created() {
     
    },
    data(){
      return {
        
      }
    }

}
</script>