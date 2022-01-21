<template>
    <header>
        <div class="head-container">
            <div class="logo">
                <img src="../assets/img/netflix-logo.png" alt="Netflix">
            </div>
            <div class="search">
                <input type="text" name="text" id="text" placeholder="Search" v-model="inputText" @keyup.enter="runSearch()">
                <button @click="$emit('compileInfo', cards)" class="btn">Cerca</button>
            </div>
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
            cards: [],
            movies: [],
            Tvs: [],
            queryLink: 'https://api.themoviedb.org/3/search/',
            queryTv: 'https://api.themoviedb.org/3/search/tv',
            apiKey: '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: 'it-IT',
        }
    },
    created() {
       
    },
    methods: {
        runSearch() {
            let queryLink = this.queryLink;
            let endpointMovie = 'movie';
            let endpointTv = 'tv';
            let parameters = {
                api_key: this.apiKey,
                language: this.lang,
                query: this.inputText
            }
            axios
            .get(`${queryLink}${endpointMovie}`, {params: parameters})
            .then(result => {
                this.movies = result.data.results;
                axios
                .get(`${queryLink}${endpointTv}`, {params: parameters})
                .then(result => {
                    this.Tvs = result.data.results;
                    this.cards = this.movies.concat(this.Tvs);
                })
                .catch(error => {
                    console.log(error);
                });
            })
            .catch(error => {
                console.log(error);
            });
        }
    }
}
</script>

<style lang="scss">
 .head-container {
     width: 100%;
     height: 100px;
     display: flex;
     justify-content: space-between;
     align-items: center;
     padding: 1em 2em;
     background-color: black;
     .logo {
         width: 20%;
         img {
             width: 50%;
             height: 80%;
         }
     }
 }
</style>