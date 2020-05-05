<template>
  <div>
    <p v-if="error">{{ error }}</p>
    <div v-for="movie in movies" :key="movie" class="gallery">
      <v-app  v-for="details in movie" :key="details">
        <v-card>
        <v-img
          class="white--text align-end"
          height="200px"
          :src="details.Poster"
        >
        <v-card-title>{{details.Title}}</v-card-title>
        </v-img>
  
        <v-card-subtitle class="pb-0">Number 10</v-card-subtitle>
    
        <v-card-text class="text--primary">
          <div>Whitehaven Beach</div>
    
          <div>Whitsunday Island, Whitsunday Islands</div>
        </v-card-text>
  
        <v-card-actions>
          <v-btn
            color="orange"
            text
          >
            Share
          </v-btn>
    
          <v-btn
            color="orange"
            text
          >
            Explore
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

import {EventBus} from '../main'
export default {
  name: "Movies",
  data() {
    return {
      movies: [],
      error: "",
      text: ''
    };
  },
  mounted() {
      EventBus.$on('my-data', data =>{
          this.movies = data
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .gallery{
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      column-gap: .8rem;
      grid-auto-rows: 400px;

     &__movies{

     }

     &__img{
       height: 250px;
       
     }
  }

</style>
