<template>
  <div>
    <p v-if="error">{{ error }}</p>
    <div v-for="movie in movies" :key="movie.Year" class="gallery">
      <v-app  v-for="details in movie" :key="details.imdbID">
        <v-card v-if="details.Poster">
          <v-img
            v-if="details.Poster"    
            class="white--text align-end"
            height="200px"
            :src="details.Poster"
          >
          </v-img>
          <v-card-subtitle class="pb-0">{{details.Title}}</v-card-subtitle>   
          <v-card-text class="text--primary">
            <div>Lançado em {{details.Year}}</div>
          </v-card-text>
          <v-card-actions>
            <v-btn
              color="orange"
              text
              @click="getDetails(details.imdbID)"
            >
              Saiba mais
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-app>
    </div>   

  </div>
</template>

<script>
import {EventBus} from '../main'
import axios from 'axios';

export default {
  name: "Movies",
  data() {
    return {
      movies: [],
      error: "",
      details: [],

    };
  },
  mounted() {
       axios.get("http://www.omdbapi.com/", {
         params: {
           apiKey: "cc8c2843",
           s: 'Movie'
         }
       })
       .then(response => {
         this.movies = response.data;
       })
       .catch(error =>{
         console.log(error);
       })
  },
  methods: {
    async getDetails(movieId){
      const res = await axios.get("http://www.omdbapi.com/",{
        params: {
          apiKey: "cc8c2843",
          i: movieId
        }
      })
      this.details = res.data
  
      EventBus.$emit('movie-details', this.details);
    
    }
  }
};
</script>

<style scoped lang="scss">
  .gallery{
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      column-gap: 1rem;
      grid-auto-rows: 400px;

     &__movies{

     }

     &__img{
       height: 250px;
       
     }
  }

</style>
