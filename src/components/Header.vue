<template>
    <header>
        <div class="head-container">
            <!-- logo -->
            <div class="logo">
                <img src="../assets/img/netflix-logo.png" alt="Netflix">
            </div>
            <!-- /logo -->

            <!-- search bar -->
            <div class="search">
                <input type="text" name="text" id="text" placeholder="Search" v-model="inputText" @keyup.enter="runSearch()">
                <button @click="$emit('compileInfo', cards)" class="btn">Cerca</button>
            </div>
            <!-- /search bar -->
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
            tvs: [],
            moviesCast: [],
            tvsCast: [],
            // api request data
            queryLink: 'https://api.themoviedb.org/3/search/',
            queryMovieCredits: 'https://api.themoviedb.org/3/movie/',
            queryTvCredits: 'https://api.themoviedb.org/3/tv/',
            apiKey: '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: 'it-IT',
        }
    },
    created() {
       
    },
    methods: {
        runSearch() { //axios request function on keyup enter 
            let queryLink = this.queryLink;
            let endpointMovie = 'movie';
            let endpointTv = 'tv';
            let parameters = {
                api_key: this.apiKey,
                language: this.lang,
                query: this.inputText
            };
            let parameters2 = {
                api_key: this.apiKey,
                language: this.lang,
            };
            axios
            .get(`${queryLink}${endpointMovie}`, {params: parameters})
            .then(result => {
                this.movies = result.data.results;
                // chiamata axios per reperire il cast dall'id per movie
                this.movies.forEach(element => {
                    let queryMovieCredits = this.queryMovieCredits
                    let endpointMovieCredits = element.id + '/credits';
                    axios
                    .get(`${queryMovieCredits}${endpointMovieCredits}`, {params: parameters2})
                    .then(result => {
                        // aggiungo il cast all'oggetto relativo ad ogni movie
                        element.cast = result.data.cast.splice(0, 5);
                        //chiamata axios per reperire i generi associati al movie
                        let endpointMovieDetails = element.id;
                        axios
                        .get(`${queryMovieCredits}${endpointMovieDetails}`, {params: parameters2})
                        .then(result => {
                            //aggiungo i generi all'oggetto relativo al movie
                            element.genres = result.data.genres;
                        })
                        .catch(error => {
                            console.log(error);
                        });
                        
                    })
                    .catch(error => {
                        console.log(error);
                    });
                });
                // chiamata per le tvs
                axios
                .get(`${queryLink}${endpointTv}`, {params: parameters})
                .then(result => {
                    this.tvs = result.data.results;
                    // chiamata axios per reperire il cast dall'id per tvs
                    this.tvs.forEach(element => {
                        let queryTvCredits = this.queryTvCredits
                        let endpointTvCredits = element.id + '/aggregate_credits';
                        axios
                        .get(`${queryTvCredits}${endpointTvCredits}`, {params: parameters2})
                        .then(result => {
                            // aggiungo il cast all'oggetto relativo ad ogni serie
                            element.cast = result.data.cast.splice(0, 5);
                            //chiamata axios per reperire i generi associati al movie
                            let endpointTvDetails = element.id;
                            axios
                            .get(`${queryTvCredits}${endpointTvDetails}`, {params: parameters2})
                            .then(result => {
                                //aggiungo i generi all'oggetto relativo al movie
                                element.genres = result.data.genres;
                            })
                            .catch(error => {
                                console.log(error);
                            });
                        })
                        .catch(error => {
                            console.log(error);
                        });
                    });
                    this.cards = this.movies.concat(this.tvs);
                    console.log(this.cards);
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
@import '../assets/scss/partials/_mixins.scss';

 .head-container {
     width: 100%;
     height: 10vh;
     @include flex(space-between, center, nowrap);
     padding: 1em 2em;
     background-color: black;
     .logo {
         height: 100%;
         width: 20%;
         img {
             width: 40%;
             height: 100%;
         }
     }
 }
</style>