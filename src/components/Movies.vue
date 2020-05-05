<template>
  <div>
    <p v-if="error">{{ error }}</p>
    <input type="text" name="search" id="search" v-model="mySearch" />
    <button class="btn" @click="getMovies">Search</button>
    <div v-for="movie in movies" :key="movie">
      <p v-for="details in movie" :key="details">
        {{ details.Title }}
        {{ details.Poster }}
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Movies",
  data() {
    return {
      movies: [],
      error: "",
      mySearch: ""
    };
  },
  methods: {
    getMovies() {
      axios
        .get("http://www.omdbapi.com/", {
          params: {
            apiKey: "cc8c2843",
            s: this.mySearch
          }
        })
        .then(response => {
          this.movies = response.data;
        })
        .catch(error => {
          this.error = error;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
#search {
  outline: none;
  border: 1px solid #ccc;
  padding: 1rem 2rem;
}

.btn {
  padding: 1rem 2rem;
  border: none;
  background-color: rgb(106, 143, 212);
  text-transform: uppercase;
}
</style>
