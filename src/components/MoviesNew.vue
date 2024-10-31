<script>
 export default {
  data: function () {
    return {
      newMovieParams: {},
    };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("createMovie", this.newMovieParams);
      this.newMovieParams = {};
    },
  },
 };
</script>

<template>
  <div>
    <h1>New Movies</h1>
    <form v-on:submit.prevent="handleSubmit">
      <div>
        Name:
        <input type="text" v-model="newMovieParams.name"/>
      </div>
      <div>
        Year:
        <input type="text" v-model="newMovieParams.year"/>
      </div>
      <div>
        Genre:
        <input type="text" v-model="newMovieParams.genre"/>
      </div>
      <button type="submit">Create Movie</button>
    </form>
  </div>
</template>

<style></style>