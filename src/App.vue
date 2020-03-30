<template>
  <div id="app">
    <div class="container">
      <div class="heading">
        <h2>Movie Reviews</h2>
        <h6 class="subheader">
          While your at home, find movies and review movies
        </h6>
      </div>
      <div class="row">
        <div class="columns small-7">
          <movie></movie>
        </div>
        <div class="columns small-5">
          <review></review>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Movie from "./components/Movie.vue";
import Review from "./components/Review.vue";
export default {
  name: "App",
  components: {
    Movie,
    Review
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
