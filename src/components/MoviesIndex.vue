<script>
export default {
  props: {
    movies: Array,
  },
};
</script>

<template>
  <div>
    <h1>All MOVIES</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{movie.name}}</h2>
      <p> Year: {{ movie.year }}</p>
      <p> Genre: {{ movie.genre }}</p>
      <button v-on:click="$emit('showMovie', movie)"> Show More </button>
    </div>
  </div>
</template>

<style></style>