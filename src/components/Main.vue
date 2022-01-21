<template>
    <main>
        <div>
            <Card v-for="(card, index) in cards"
            :key="index"
            :title="card.title || card.name"
            :originalTitle="card.original_title || card.original_name"
            :language="card.original_language"
            :vote="voteCorrector(card.vote_average)"
            :poster="posterLink + card.poster_path"
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
            posterLink: 'https://image.tmdb.org/t/p/w92/',
        }
    },
    props: {
        cards: {
            type: Array,
        }
    },
    methods: {
        voteCorrector(number) {
            let vote = Math.ceil((number * 5) / 10);
            return vote;
        }
    }
}
</script>

<style>

</style>