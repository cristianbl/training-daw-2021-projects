<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/cart">Carrito</router-link> |
      <router-link to="/productdetail"> Detalle de Producto</router-link>
    </div>
    <h1 v-if="isMock">Working with MOCK data</h1>
    <router-view/>
  </div>
</template>

<script>
export default {
  computed: {
    isMock() {
      return process.env.VUE_APP_API_IS_MOCK === "true"
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
