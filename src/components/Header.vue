<template>
  <div>
      <input type="text" name="text" id="text" placeholder="Search" v-model="inputText" @keyup.enter="runSearch()">
      <button @click="$emit('compileInfo', movies)" class="btn">Cerca</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Header",
    data() {
        return {
            inputText: '',
            movies: [],
            queryApi: 'https://api.themoviedb.org/3/search/movie',
            apiKey: '?api_key=' + '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: '&language=',
            query: '&query=',
        }
    },
    created() {
       
    },
    methods: {
        runSearch() {
            axios
            .get(this.queryApi+this.apiKey+this.lang+'it-IT'+this.query+this.inputText)
            .then(result => {
                console.log(result.data.results);
                this.movies = result.data.results;
            })
            .catch(error => {
                console.log(error);
            });
        }
    }
}
</script>

<style>

</style>