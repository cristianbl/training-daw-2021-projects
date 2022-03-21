<template>
    <div>
    <h4>{{item.name}}</h4>
    <img class="img" :src="item.mainImage" />
      <h5 class="price"> Price: ${{item.price}}</h5>
      <p class="description">Description: {{item.description}} </p>
      <router-link :to="{name: 'ProductDetail', params: {id: item.id}}">
        <button>Ver</button>
      </router-link>
      <button @click="add()">Añadir Carrito</button>
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
    },
    methods: {
        async add(){
            console.log(this.item.id)
            // promise to object
            let orderProduct = await this.getProductFromCart(this.item.id)
            console.log(orderProduct);
            if(orderProduct != null){
                console.log(`PUT ${this.id}`);
                let p = await this.getProductFromCart(this.item.id)
                var xhr = new XMLHttpRequest();
                xhr.open("PUT", `http://localhost:3000/cart/${p.id}`, true);
                xhr.setRequestHeader('Content-Type', 'application/json');
                xhr.send(JSON.stringify({
                    item: this.item,
                    quantity: p.quantity + 1
                }));
                this.qty+=1;
            }else{
                console.log(`POST ${this.id}`);
                xhr = new XMLHttpRequest();
                xhr.open("POST", 'http://localhost:3000/cart', true);
                xhr.setRequestHeader('Content-Type', 'application/json');
                xhr.send(JSON.stringify({
                    item: this.item,
                    quantity: 1
                }));
                this.qty=1;
            }
        },
        getProductFromCart(id){
          let data = fetch('http://localhost:3000/cart')
            .then(response=> response.json())
            .then(data=> data.filter(item => item.item.id == id))
            .then(data=> {
                if(data.length > 0){
                    return data[0]
                }else{
                    return null
                }
            })
            return data
        }
    },

}
</script>