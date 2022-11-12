
<template>
  <Pokemon_page/>
</template>

<script>
import Pokemon_page from './pages/Pokemon_page.vue';

export default {
  name: 'App',
  components: {
    Pokemon_page
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color:white;
  background-image: url("https://wallpapercave.com/wp/wp3170170.jpg");
  background-repeat: no-repeat, repeat;
  background-color: #cccccc;
  background-size: cover; 
  height: 100vh;
  display: flex;
  background-attachment: fixed;
  align-items: center;
 
  
}


</style>



