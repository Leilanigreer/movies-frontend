<script>
import axios from "axios";
axios.defaults.headers.post = axios.defaults.headers.patch = {
    'Content-Type': 'application/x-www-form-urlencoded'
  };
import MoviesIndex from "./MoviesIndex.vue"
import MoviesNew from "./MoviesNew.vue"

export default {
  components: {
    MoviesIndex,
    MoviesNew,
  },
  data: function () {
    return {
      movies: [],
    };
  },
  created: function () {
    this.handleIndexMovies();
  },
  methods: {
    handleIndexMovies: function () {
      axios.get("http://localhost:5000/movies.json").then((response) => {
        console.log("movies index", response);
        this.movies = response.data;
      });
    },
    handeCreateMovie: function (params) {
      axios 
        .post("http://localhost:5000/movies.json", params)
        .then((response) => {
          console.log("movies create", response);
          this.movies.push(response.data)
        })
        .catch((error) => {
          console.log("movies create error", error.response);
        });
    },
  },
};
</script>

<template>
  <main>
    <MoviesNew v-on:createMovie="handeCreateMovie"/>
    <MoviesIndex v-bind:movies="movies" />
  </main>
</template>

<style></style>