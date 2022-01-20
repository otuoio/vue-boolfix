<template>
    <main>
        <div>
            <Card v-for="(movie, index) in movieFind"
            :key="index"
            :title="movie.title || movie.name"
            :originalTitle="movie.original_title || movie.original_name"
            :language="movie.original_language"
            :vote="movie.vote_average"
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
        getFlags(lan) {
            if (lan === 'en') {
                return 'gb';
            } else if (lan === 'ja') {
                return 'jp';
            } else {
                return lan;
            };
        }
    }
}
</script>

<style>

</style>