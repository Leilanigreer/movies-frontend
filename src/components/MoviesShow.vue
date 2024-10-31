<script>
export default {
  props: {
    movie: Object,
  },
};
</script>

<template>
  <div>
    <h1>Movie information</h1>
    <p>Name: {{ movie.name }}</p>
    <p>Year: {{ movie.year }}</p>
    <p>Genre: {{ movie.genre }}</p>
  </div>
</template>

<style></style>