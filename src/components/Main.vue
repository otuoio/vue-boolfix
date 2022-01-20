<template>
    <main>
        <div>
            <Card v-for="(movie, index) in movieFind"
            :key="index"
            :title="movie.title || movie.name"
            :originalTitle="movie.original_title || movie.original_name"
            :language="movie.original_language"
            :vote="movie.vote_average"
            :poster="pathCorrector(movie.poster_path)"
            :alt="movie.original_title || movie.original_name"
            />
        </div>
    </main>
</template>

<script>
import Card from './Card.vue'

export default {
    name: "Main",
    components: {
        Card
    },
    data() {
        return {

        }
    },
    props: {
        movieFind: {
            type: Array,
        }
    },
    created() {
        
    },
    computed: {
        
    },
    methods: {
        pathCorrector(path) {
            if (path === null) {
                return null;
            } else {
                return 'https://image.tmdb.org/t/p/w92/'+path;
            }
        }
    }
}
</script>

<style>

</style>