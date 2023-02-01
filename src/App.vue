<template>  
  <GetDogs />
  <DogDetails></DogDetails> 
</template>

<script>
import GetDogs from './components/GetDogs.vue'
import DogDetails from './components/DogDetails.vue'  

//const API_KEY = "live_zp98sjWc8WpkkxNXJ5feMRMMDpe1dw5KNMC33VRxxGQXC9z06a5dlWMYouk4yLHj";

export default {
  name: 'App',
  components: {
    GetDogs,
    DogDetails,  
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
  margin-top: 60px;
  word-wrap:break-word;
}
</style>
