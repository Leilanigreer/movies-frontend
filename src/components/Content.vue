<script>
import axios from "axios";
axios.defaults.headers.post = axios.defaults.headers.patch = {
    'Content-Type': 'application/x-www-form-urlencoded'
  };
import MoviesIndex from "./MoviesIndex.vue"
import MoviesNew from "./MoviesNew.vue"
import MoviesShow from "./MoviesShow.vue";
import Modal from "./Modal.vue"

export default {
  components: {
    MoviesIndex,
    MoviesNew,
    MoviesShow,
    Modal,
  },
  data: function () {
    return {
      movies: [],
      currentMovie: {},
      isMoviesShowVisible: false,
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
    handleShowMovie: function (movie) {
      console.log ("handleShowMovie", movie);
      this.currentMovie = movie;
      this.isMoviesShowVisible = true;
    },
    handleClose: function () {
      this.isMoviesShowVisible = false;
    },
  },
};
</script>

<template>
  <main>
    <MoviesNew v-on:createMovie="handeCreateMovie"/>
    <MoviesIndex v-bind:movies="movies" v-on:showMovie="handleShowMovie"/>
    <Modal v-bind:show="isMoviesShowVisible" v-on:close="handleClose">
      <MoviesShow v-bind:movie="currentMovie"/>
    </Modal>
  </main>
</template>

<style></style>