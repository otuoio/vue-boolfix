<template>
  <div class="container">
      <ul v-for="(movie, index) in movies"
          :key="index">
          <li>
              {{ movie.title}}
          </li>
          <li>
              {{ movie.original_title}}
          </li>
          <li>
              {{ movie.original_language}}
          </li>
          <li>
              {{ movie.vote_count}}
          </li>
      </ul>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Main",
    data() {
        return {
            movies: [],
            queryApi: 'https://api.themoviedb.org/3/search/movie',
            apiKey: '?api_key=' + '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: '&language=',
            query: '&query='
        }
    },
    created() {

        axios
        .get(this.queryApi+this.apiKey+this.lang+'it-IT'+this.query+'batman')
        .then(result => {
            console.log(result.data.results);
            this.movies = result.data.results;
        })
        .catch(error => {
            console.log(error);
        });
    }
}
</script>

<style>

</style>