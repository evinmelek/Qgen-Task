<template>  
  <GetDogs />
  <DogDetails></DogDetails> 
</template>

<script>
import GetDogs from './components/GetDogs.vue'
import DogDetails from './components/DogDetails.vue'  

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
