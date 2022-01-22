<template>
    <main>
        <div class="cards">
            <Card v-for="(card, index) in cards"
            :key="index"
            :title="card.title || card.name"
            :originalTitle="card.original_title || card.original_name"
            :language="card.original_language"
            :vote="voteCorrector(card.vote_average)"
            :poster="posterLink + card.poster_path"
            :alt="card.original_title || card.original_name"
            :overview="card.overview"
            :cast="card.cast"
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
            posterLink: 'https://image.tmdb.org/t/p/w342/',
        }
    },
    props: {
        cards: {
            type: Array,
        }
    },
    methods: {
        voteCorrector(number) {//vote from 10 to 5 function
            let vote = Math.ceil((number * 5) / 10);
            return vote;
        }
    }
}
</script>

<style lang="scss">
@import '../assets/scss/partials/_variables.scss';
@import '../assets/scss/partials/_mixins.scss';

.cards {
    width: 100%;
    height: 90vh;
    background-color: $bg-gray;
    overflow-y: auto;
    @include flex(flex-start, start, wrap);
}
</style>