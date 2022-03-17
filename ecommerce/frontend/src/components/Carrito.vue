<template>
  <div v-if="quantity>0" style="border:1px solid black; width: 70% ; margin:auto; margin-top:10px;">

      <h2>{{item.name}}</h2>
      <img :src="item.mainImage" />
      <p>{{item.short}}</p>
      <h5>Cantidad: {{quantity}}</h5>
      <button @click="remove() ">Remove</button>
  </div>
</template>

<script>
export default {
    props:[
        'item',
        'quantity'
    ],
    methods:{
        async remove(){
            let p = await this.getProductFromCart(this.item.id)

            if(this.getProductFromCart(this.item.id) && p.quantity > 1){

                var xml = new XMLHttpRequest();
                xml.open("PUT", `http://localhost:3000/cart/${p.id}`, true);
                xml.setRequestHeader('Content-Type', 'application/json');
                xml.send(JSON.stringify({
                    item: this.item,
                    quantity: p.quantity - 1
                }));
                this.quantity-=1
                this.$forceUpdate();

            }else{
                xml = new XMLHttpRequest();
                xml.open("DELETE", `http://localhost:3000/cart/${p.id}`, true);
                xml.setRequestHeader('Content-Type', 'application/json');
                xml.send();
                this.quantity=null
                this.$forceUpdate();

            }
        },getProductFromCart(id){
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


    }


}
</script>

<style>

</style>