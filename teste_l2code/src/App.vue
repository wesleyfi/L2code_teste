<template>
  <div id="app">
    <Comparador/>
  </div>
</template>

<script>
import Comparador from './components/Comparador.vue'

export default {
  name: 'App',
  components: {
    Comparador
  }
}
</script>

<style>
body{
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}
#app {
  
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #000000;
  
}
</style>
