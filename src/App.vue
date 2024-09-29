<template>
  <HeaderComp/>
  <router-view></router-view>
</template>

<script>
import HeaderComp from './components/HeaderComp.vue';

export default {
  name: 'App',
  components: {
    HeaderComp
}
}
</script>

<style>
*{
  margin:0;
  padding:0;
 
}
body{
  background-color: #eeeee7;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
  
}
</style>
