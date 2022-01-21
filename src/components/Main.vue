<template>
    <main>
        <div>
            <Card v-for="(card, index) in cards"
            :key="index"
            :title="card.title || card.name"
            :originalTitle="card.original_title || card.original_name"
            :language="card.original_language"
            :vote="voteCorrector(card.vote_average)"
            :poster="pathCorrector(card.poster_path)"
            :alt="card.original_title || card.original_name"
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
        cards: {
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
        },
        voteCorrector(number) {
            let vote = Math.ceil((number * 5) / 10);
            return vote;
        }
    }
}
</script>

<style>

</style>