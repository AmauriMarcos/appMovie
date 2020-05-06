<template>
<div class="myContainer">
  <v-app>
    <v-navigation-drawer app color="blue-grey darken-1">
     
    </v-navigation-drawer>

    <v-app-bar app >
      
        <Search></Search>  
    
    </v-app-bar>

  <!-- Sizes your content based upon application components -->
    <v-content>

      <!-- Provides the application the proper gutter -->
      <v-container fluid color="blue-grey darken-4">
        <Movies></Movies>
         <Details></Details>
        <!-- If using vue-router -->
        <router-view></router-view>
      </v-container>
    </v-content>

  <v-footer app color="blue-grey darken-4" class="myFooter">
    <!-- -->
     
  </v-footer>
</v-app>
</div>
  
</template>

<script>
import Movies from "./components/Movies";
import Search from "./components/Search";
import Details from "./components/Details";

export default {
  name: "App",

  components: {
    Movies,
    Search,
    Details
  },

  data: () => ({
    //
  })
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