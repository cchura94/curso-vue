<template>
  <div id="app">
    
    <Menu></Menu>
    
    <div id="nav">
      <router-link to="/">INICIO</router-link> |
      <router-link to="/about">NOSOTROS</router-link> |
      <router-link to="/contacto">CONTACTO</router-link> |

      <router-link to="/carrito">CARRITO</router-link>
    </div>

    <router-view></router-view>    


  </div>
</template>

<script>
// @ is an alias to /src
import Menu from '@/components/Menu.vue'

export default {
  components: {
    Menu
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
