<template>
    <header>
        <div class="head-container">
            <!-- logo -->
            <div class="logo">
                <img src="../assets/img/netflix-logo.png" alt="Netflix">
            </div>
            <!-- /logo -->

            <!-- genres filter -->
            <div class="filter d-flex">
                <label for="genres text-nowrap  ">Scegli un genere </label>
                <select class="form-select bg-dark text-light" v-model="selected" @change="$emit('filterGenre', selected)" name="genres" id="genres">
                    <option value="" selected disabled hidden>Tutti i generi</option>
                    <option v-for="(genre, index) in genresList"
                    :key="index" 
                    :value="genre"
                    >
                        {{ genre }}
                    </option>
                </select>
            </div>
            
            <!-- /genres filter -->

            <!-- search bar -->
            <div class="search d-flex">
                <input class="form-control bg-dark text-light" type="text" name="text" id="text" placeholder="Inserisci titolo" v-model="inputText" @keyup.enter="runSearch()">
                <button class="btn btn-outline-danger " @click="$emit('compileInfo', cards)">Cerca</button>
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
            selected: '',
            inputText: '',
            cards: [],
            genresList: [],
            movies: [],
            tvs: [],
            moviesCast: [],
            tvsCast: [],
            // api request data
            queryLink: 'https://api.themoviedb.org/3/search/',
            queryGenres: 'https://api.themoviedb.org/3/genre/',
            queryMovieCredits: 'https://api.themoviedb.org/3/movie/',
            queryTvCredits: 'https://api.themoviedb.org/3/tv/',
            apiKey: '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: 'it-IT',
        }
    },
    created() {
        this.searchGenres();
    },
    methods: {
        searchGenres() {
            let queryGenres = this.queryGenres;
            let endpointGenresMovie = 'movie/list';
            let endpointGenresTv = 'tv/list';
            let parameters2 = {
                api_key: this.apiKey,
                language: this.lang,
            };
            axios//chiamata per i generi movie
            .get(`${queryGenres}${endpointGenresMovie}`, {params: parameters2})
            .then(result => {
                // array con la lista dei generi dei movie
                result.data.genres.forEach(element => {
                    this.genresList.push(element.name);
                });

                axios//chiamata per i generi tv
                .get(`${queryGenres}${endpointGenresTv}`, {params: parameters2})
                .then(result => {
                    // ciclo sugli elementi dell'array con i generi dei tvs e, se l'elemento non è ancora contenuto nell'array dei generi, lo pusho
                    result.data.genres.forEach(element => {
                        if (!(this.genresList.includes(element.name))) {
                            this.genresList.push(element.name);
                        }
                    });
                    console.log(this.genresList);
                })
                .catch(error => {
                    console.log(error);
                });
            })
            .catch(error => {
                console.log(error);
            });
        },
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
     label {
         color: gray;
     }
 }
</style>