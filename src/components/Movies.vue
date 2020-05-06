<template>
  <div>
    <p v-if="error">{{ error }}</p>
    <div v-for="movie in movies" :key="movie" class="gallery">
      <v-app  v-for="details in movie" :key="details">
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
            @click='getDetailsMovie(details.imdbID)'
          >
            Saiba mais
          </v-btn>
        </v-card-actions>
       
    </v-card>
      </v-app>
      <!-- <div class="gallery__movies">
        <h2>{{ details.Title }}</h2>
        <img :src="details.Poster " class="gallery__img">
      </div> -->
    </div>
    
  </div>
</template>

<script>
import axios from 'axios';
import {EventBus} from '../main';

export default {
  name: "Movies",
  data() {
    return {
      movies: [],
      error: "",
      text: '',
      detailsMovie: []
    };
  },
  mounted() {
      EventBus.$on('my-data', data =>{
          this.movies = data
      });
  },
  methods: {
     getDetailsMovie(movieId){
       axios.get("http://www.omdbapi.com/", {
         params: {
           apiKey: "cc8c2843",
           i: movieId
         }
       })
       .then(response => {
         this.detailsMovie = response.data
       })
       .catch(error =>{
         console.log(error);
       })

       EventBus.$emit('details-movie', this.detailsMovie)
     }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
