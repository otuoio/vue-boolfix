<template>
  <div class="card">
      <div @mouseover="showInfo = true" @mouseleave="showInfo=false" class="poster">
          <img v-if="isNull(poster)" :src="poster" :alt="alt">
          <div v-else class="not-poster">
              {{ originalTitle}}
          </div>
      </div>
      <div v-show="showInfo" class="info">
          <h2 class="title">Title: {{ title }}</h2>
        <h3 class="org_title">Original Title: {{ originalTitle }}</h3>
        <div class="flag">
            <country-flag v-if="isAvailable()" :country='getFlags(language)' size='small' shadow />
            <span v-else>{{ language }}</span>
        </div>
        <div class="vote">
          <font-awesome-icon v-for="(item, index) in votes"
            :key="index" :icon="[votesArray(index, vote), 'star']" /> 
        </div>
        <p><b>Overview: </b>{{ overview }}</p>
        </div>
  </div>
</template>

<script>
export default {
    name: 'Card',
    compontent: {

    },
    data() {
        return {
            votes: [
                1,
                2,
                3,
                4,
                5
            ],
            languages: [
                'it',
                'en',
                'es',
                'de',
                'fr'
            ],
            showInfo: false,
        }
    },
    props: {
        title: {
            type: String,
        },
        originalTitle: {
            type: String,
        },
        language: {
            type: String,
        },
        vote: {
            type: Number,
        },
        poster: {
            type: String,
        },
        alt: {
            type: String,
        },
        overview: {
            type: String,
        }
    },
    methods: {
        isNull(item) {
            if (item !== 'https://image.tmdb.org/t/p/w342/null') {
                return true;
            }
        },
        isAvailable() {
            if (this.languages.includes(this.language)) {
                return true;
            } else {
                return false;
            }
        },
        getFlags(lan) {
            if (lan === 'en') {
                return 'gb';
            } else if (lan === 'ja') {
                return 'jp';
            } else {
                return lan;
            };
        },
        votesArray(index, number) {
            if (index < number) {
                return 'fas';
            } else {
                return 'far';
            }
        }
    }
}
</script>

<style lang="scss">
@import '../assets/scss/partials/_mixins.scss';

.card {
    flex-basis: 22%;
    text-align: center;
    .poster {
        height: 70vh;
        border: 1px solid white;
        img {
            width: 100%;
            height: 100%;
        }
    }
}
</style>