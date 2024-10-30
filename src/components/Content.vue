<script>
import axios from "axios";
import MoviesIndex from "./MoviesIndex.vue"

export default {
  components: {
    MoviesIndex,
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
  },
};
</script>

<template>
  <main>
    <MoviesIndex v-bind:movies="movies" />
  </main>
</template>

<style></style>