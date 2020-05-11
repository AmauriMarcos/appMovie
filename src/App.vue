<template>
<div>
  <div class="barra">
     <div class="barra__box">
        <div class="barra__box-back">
            <h3>&larr; Back</h3>
        </div>
        
        <input type="text" class="barra__box-myInput" v-model="query">
         
        <button class="barra__box-btn" @click='updateQuery'>Search</button>
        
     </div>
  </div>

<div class="myContainer">
   
  <div class="poster">
      <img :src="details.Poster">
  </div>
  <div :class="active? 'movieA':'movieB'">
        <Movies v-if='show'></Movies>
        <div v-else>
          <v-app>
            <v-card :loading="loading" >    
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
  </div>
</div>
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
      note: 'Bom',
      active: true,
    }
  },
  mounted(){
    EventBus.$on('movie-details', data =>{
    this.details = data;
    this.active = false
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
    display: grid;
    grid-template-columns: repeat(6, 1fr);
  }

  .poster{
    grid-column: 1/2;
    align-self: center;
  }

  .movieA{
    grid-column: 1/-1;
  }
  .movieB{
    grid-column: 2/-1;
  }
  .myFooter{
    height: 50px !important;
  }
  
  .v-application--wrap{
    min-height: 0 !important;
  }


  .barra{
    background: linear-gradient(to right, #ACA6CA, #AE6DAB);
    padding:  2% 7%;

    &__box{
      display: grid !important;
      grid-template-columns: 1fr 3fr 1fr;

      &-back{
        color: #F1EFF9;
      }

      &-myInput{
        border: 1px solid #ccc;
        width: 100% !important;
        background-color: #F1EFF9;
        outline: none;
        grid-column: 2/3;
      }

      &-btn{
        justify-self: start;
        padding: 3px 13px;
        background-color: #F1EFF9;
        outline: none;

        &:hover{
          background-color: #00C2CF;
          
        }
      }
      
    }
  }


</style>