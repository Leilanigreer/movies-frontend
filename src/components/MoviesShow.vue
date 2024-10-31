<script>
export default {
  props: {
    movie: Object,
  },
  data: function () {
    return {
      editMovieParams: {},
    };
  },
  created: function () {
    console.log("FIRST", this.movie);
    console.log("SECOND", { ...this.movie });
    this.editMovieParams = { ...this.movie };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("updateMovie", this.movie.id, this.editMovieParams);
    },
  },
};
</script>

<template>
  <div>
    <h1>Movie information</h1>
    <p>Name: {{ movie.name }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Genre: {{ movie.genre }}</p>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Name:
        <input v-model="editMovieParams.name" type="text" />
      </div>
      <div>
        Year:
        <input v-model="editMovieParams.year" type="text" />
      </div>
      <div>
        Genre:
        <input v-model="editMovieParams.genre" type="text" />
      </div>
      <button type="submit">Update Movie</button>
    </form>
    <button v-on:click="$emit('destroyMovie', movie)">Destroy movie</button>
  </div>
</template>

<style></style>