<template>
  <div>
    <h2>Dog List</h2>
    <div>
      <label for="breed-select">Filter by breed:</label>
      <select id="breed-select" v-model="selectedBreed" @change="filterDogsByBreed"> 
        <option v-for="breed in breeds" :key="breed" :value="breed">{{ breed }}</option>
      </select>
    </div>
    <ul class="dog-list">
      <li class="list-element" v-for="dog in displayedDogs" :key="dog.id">
        {{ dog.name }}
        <img v-if="dog.photo" :src="dog.image" alt="dog photo">
        <button class="detail-button" @click="viewDetails(dog)">View Details</button>
      </li>
    <div>
      <button class="page-button" @click="previousPage" :disabled="currentPage === 1">Previous</button>
      <button class="page-button" @click="nextPage" :disabled="currentPage === maxPage">Next</button>
    </div>
    </ul>
    <dog-details
      v-if="selectedDog"
      :dog="selectedDog"
      :admin="admin"
      @close="selectedDog = null"
    ></dog-details>
    <div v-if="admin">
      <h3>Timeline</h3>
      <ul>
        <li v-for="event in selectedDog.timeline" :key="event.id">
          {{ event.date }}: {{ event.description }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import DogDetails from './DogDetails.vue';

export default {
  components: {
    DogDetails
  },
  data() {
      return {
        dogs: [],
        selectedDog: null,
        selectedBreed:"", 
        breeds: [], 
        currentPage: 1,
        itemsPerPage: 10,
        admin: false
      }
    },
    computed: {
    events() {
      return this.dog.timeline || []
    },
      displayedDogs() {
        if (!this.selectedBreed) {
          return this.dogs.slice((this.currentPage - 1) * this.itemsPerPage, this.currentPage * this.itemsPerPage);
        } else {
          return this.dogs
            .filter(dog => dog.breed_group === this.selectedBreed)
            .slice((this.currentPage - 1) * this.itemsPerPage, this.currentPage * this.itemsPerPage);
        }
      },
      maxPage() {
        return Math.ceil(this.dogs.length / this.itemsPerPage);
      }
    },
  created() {
    axios.get('https://api.thedogapi.com/v1/breeds/')
      .then(response => {
        this.dogs = response.data;
        this.breeds = Array.from(new Set(this.dogs.map(dog => dog.breed_group)));
      })
      .catch(error => {
        console.log(error);
      });  
     //this.admin = true;
    
    axios.get('https://api.thedogapi.com/v1/images/')
      .then(response => {
        this.dogs = response.data;
      })
      .catch(error => {
        console.log(error);
      });
  },
  methods: { 
    viewDetails(dog) {
      this.selectedDog = dog;
    },
    filterDogsByBreed() {
      this.currentPage = 1;
    },
    previousPage() {
      this.currentPage--;
    },
    nextPage() {
      this.currentPage++;
    }
  }, 
}
</script>

<style scoped> 
h2{
  position: sticky;
  top: 0%;
}
.page-button{
  position: sticky;
  right: 0px;
  background-color: brown;
  border: brown;
  border-radius: 5px;
  padding: 1%;
  margin: 2%;
  color: white;
}
.dog-list{
  list-style-type: none;
  height: 90%;
  width: 50%;
  right: 0px;
  bottom: 0px; 
  float: right; 
  border: 1px solid silver;
}

.list-element{
  margin: 4%;
  width: 80%;
  text-align: left;
  float: left;
  border: 1px solid grey;
  border-radius: 10px;
  padding: 4%;
}

.detail-button{
  margin-right: 1%;
  float: left;
  width: 20%;
  color: antiquewhite;
  background-color: darkolivegreen;
  border: darkolivegreen;
  border-radius: 5px;
  padding: 2%;
}
ul{
  list-style-type: none;
}
</style>
