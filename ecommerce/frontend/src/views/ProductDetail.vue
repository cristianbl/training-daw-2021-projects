<template>
  <div>

    <div class="home">
      <img class="img" :src="item.mainImage" />
      <div>
        
         <h1>{{item.name}}</h1>
          <p>{{item.description}}</p>
          <p>{{item.price}}</p>
          <button @click="add()">Añadir Carrito</button>
          
          
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {

    name: "ProductDetail",
    components:{
      
    },

    data(){
        
        

        return {
            item:{}
        }
    },
    created(){
        let url = `http://localhost:3000/products/${this.id}`;
        console.log(url)
        fetch(url)
        .then(json=> json.json())
        .then(data=> this.item = data)
    },
    props: {
   
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
            .then(data=> data.filter(item=> item.item.id == id))
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
    computed:{
       id(){
           return this.$route.params.id
       }
    }
  };
</script>
<style>

</style>

