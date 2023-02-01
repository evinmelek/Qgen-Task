<template>
    <div class="card">
      <img class="dog-image"  :src="dog.image.url" alt="dog photo"/> 
      <h2>{{ dog.name }}</h2> 
      <p>Id: {{ dog.id }}</p>  
      <p v-if="dog.breed_group"><span style="font-weight:bold;">Breed:</span> {{ dog.breed_group }} </p>
      <p>{{ dog.life_span }} average life span</p> 
      <p>{{ dog.bred_for }}</p>
      <button class="close-button" @click="$emit('close')">Close</button>
    </div>
</template>
  
<script> 
  export default {
    props: {  
    dog: Object, 
    }
  }
</script>

<style scoped>
.card{
  height: 60%;
  width: 20%;
  text-align: left;
  border: 1px solid grey;
  border-radius: 10px;
  margin: 5%;
  padding: 4%;
  font-size: 90%;
  background-color: rgb(137, 204, 137);
}

.dog-image{
  width: 99%;
  height: auto;
  margin: 1%;
}

.close-button{
  background-color: darkslategray;
  border: darkslategray;
  border-radius: 15%;
  padding: 3%;
  color: white;
}
</style>
  