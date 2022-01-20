<template>
    <header>
        <div>
            <input type="text" name="text" id="text" placeholder="Search" v-model="inputText" @keyup.enter="runSearch()">
            <button @click="$emit('compileInfo', movies)" class="btn">Cerca</button>
        </div>
    </header>
</template>

<script>
import axios from 'axios';


export default {
    name: "Header",
    data() {
        return {
            inputText: '',
            shows: [],
            movies: [],
            queryMovie: 'https://api.themoviedb.org/3/search/movie',
            queryTv: 'https://api.themoviedb.org/3/search/tv',
            apiKey: '?api_key=' + '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: '&language=',
            query: '&query=',
        }
    },
    created() {
       
    },
    methods: {
        runSearch() {
            // let endpoint = 'movie';
            // let parameters = {
            //     apiKey: this.apiKey,
            //     language: 'it-IT',
            //     query: this.inputText
            // };
            axios
            .get(this.queryMovie+this.apiKey+this.lang+'it-IT'+this.query+this.inputText)
            .then(result => {
                this.shows = result.data.results;
                
                axios
                .get(this.queryTv+this.apiKey+this.lang+'it-IT'+this.query+this.inputText)
                .then(result => {
                    this.movies = this.shows.concat(result.data.results);
                    console.log(this.movies);
                })
                .catch(error => {
                    console.log(error);
                });
            })
            .catch(error => {
                console.log(error);
            });
        },
    }
}
</script>

<style>

</style>