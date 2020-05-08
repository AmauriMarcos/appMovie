<template>
<div class="myContainer">
  <v-app>
    <v-navigation-drawer app color="blue-grey darken-1" v-if='!show'>
       <v-app>
          <v-img   
            aspect-ratio="2"
            :src="details.Poster"
          ></v-img>      
       </v-app>
    </v-navigation-drawer>
         
    <v-app-bar app v-if="show">
      
    </v-app-bar>
    
    <v-content>
      <v-container fluid color="blue-grey darken-4">
        <Movies v-if='show'></Movies>
        <div v-else>
          <v-app>
            <v-card
              :loading="loading"
              class="mx-auto my-12"
            >
              
              <v-card-title>{{details.Title}}</v-card-title>
          
              <v-card-text>
                <v-row
                  align="center"
                  class="mx-0"
                >
                <div class="text-center">
                  <v-rating
                    v-model="details.imdbRating"
                    :length="length"
                    color="red lighten-3"
                    background-color="grey lighten-1"
                    small
                  ></v-rating>
                </div>
                
                <div class="grey--text ml-4">{{details.imdbRating}}</div>
                </v-row>

                <!-- Statement block of note -->
                <div v-if="details.imdbRating <= 3.5">
                  <p>{{note = 'Bad'}}</p>
                </div>
                <div v-else-if="details.imdbRating > 3.5 && details.imdbRating <= 5.5">
                  <p>{{note = 'Reasonable'}}</p>
                </div>
                <div v-else-if="details.imdbRating > 5.5 && details.imdbRating <= 8.5">
                  <p>{{note = 'Good'}}</p>
                </div>
                <div v-else-if="details.imdbRating > 8.5 && details.imdbRating <= 10">
                  <p>{{note = 'Great'}}</p>
                </div>
                <!-- BLOCK ENDs -->

                <div class="my-4 subtitle-1">
                  <p>Launched in {{details.Released}}</p>
                </div>
                <div>
                  <p>{{details.Plot}}</p>
                </div>
                <div>
                  <p>Awards: {{details.Awards}}</p>
                </div>
                <div>
                  <p>Duration: {{details.Runtime}}</p>
                </div>
                <div>
                  <p>Actors: {{details.Actors}}</p>
                </div>
                <div>
                  <p>Country: {{details.Country}}</p>
                </div>
                <div>
                  <p>Production: {{details.Production}}</p>
                </div>
              </v-card-text>
          
              <v-divider class="mx-4"></v-divider>
          
            </v-card>
          </v-app>
        </div>
        
      </v-container>
    </v-content>

  <v-footer app color="blue-grey darken-4" class="myFooter">
    <!-- -->
     
  </v-footer>
</v-app>
</div>
  
</template>

<script>

import {EventBus} from './main'
import Movies from "./components/Movies";

export default {

  name: "App",
  components: {
    Movies
  },
  data(){
    return{
      details: [],
      show: 'true',
      length: 10,
      rating: 0,
      note: 'Bom'
    }
  },
  mounted(){
      EventBus.$on('movie-details', data =>{
      this.details = data
      });
  },
  watch: {
    details(){
      this.show = false
    }
  }
};
</script>

<style lang="scss">
  .myContainer{
    padding: 3% 15%;
  }

  .myFooter{
    height: 50px !important;
  }
  
</style>