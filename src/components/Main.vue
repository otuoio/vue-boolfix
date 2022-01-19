<template>
  <div>ciao</div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Main",
    data() {
        return {
            queryApi: 'https://api.themoviedb.org/3/search/movie',
            apiKey: '?api_key=' + '981731b128a2c3353bf07ea0418b25f5', //mia api_key
        }
    },
    created() {

        // console.log('https://api.themoviedb.org/3/search/movie?api_key=981731b128a2c3353bf07ea0418b25f5?query=batman');
        axios
        .get('https://api.themoviedb.org/3/search/movie?api_key=981731b128a2c3353bf07ea0418b25f5?query=batman')
        .then(result => {
            console.log(result);
        })
        .catch(error => {
            console.log(error);
        });
    }
}
</script>

<style>

</style>