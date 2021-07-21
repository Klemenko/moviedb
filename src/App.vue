<template>
  <Home/>
</template>

<script>
import Home from './views/Home.vue'



export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 1380px;
  margin: auto;
}

.blue_hover:hover{
   color: rgb(1,180,228);
   cursor: pointer;
}

.mt-10{
  margin-top: 10px;
}

</style>
