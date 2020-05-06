<template>
  <div class="box">
    <input type="text" v-model="mySearch" id="search"> 
    <button class="btn" @click="getMovies">Search</button>  
  </div>  
</template>

<script>
import axios from "axios";
import {EventBus} from '../main';

export default {
  name: "Search",
  data(){
    return{
      mySearch: "",
      movies: [],
      detail: []
    }
  },
  methods:{
    getMovies() {
      axios
        .get("http://www.omdbapi.com/", {
          params: {
            apiKey: "cc8c2843",
            s: this.mySearch
          }
        })
        .then(response => {
          this.movies = response.data
        })
        .catch(error => {
          this.error = error;
        });
        
        EventBus.$emit('my-data', this.movies)
    }
  }
   
}
</script>
<style lang="scss" scoped>
  .box{
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #search {
  outline: none;
  border: 1px solid rgb(0, 0, 0);
  
}

.btn {
  padding: 1px 10px;
  border: none;
  background-color: rgb(106, 143, 212);
  margin: 1rem;
}
</style>