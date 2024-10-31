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
    handleUpdateMovie: function (id, params) {
      console.log("handleUpdateMovie", id, params);
      axios
        .patch(`http://localhost:5000/movies/${id}.json`, params)
        .then((response) => {
          console.log("movies update", response);
          this.movies = this.movies.map((movie) => {
            if (movie.id === response.data.id) {
              return response.data;
            } else {
              return movie;
            }
          });
          this.handleClose();
        })
        .catch((error) => {
          console.log("movies update error", error.response);
        });
    },
    handleDestroyMovie: function (movie) {
      axios.delete(`http://localhost:5000/movies/${movie.id}.json`).then((response) => {
        console.log("movies destroy", response);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
        this.handleClose();
      });
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
      <MoviesShow v-bind:movie="currentMovie" v-on:updateMovie="handleUpdateMovie"
      v-on:destroyMovie="handleDestroyMovie"/>
    </Modal>
  </main>
</template>

<style></style>