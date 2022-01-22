<template>
  <div class="card">
      <!-- card poster -->
      <div class="poster">
          <img v-if="isNull(poster)" :src="poster" :alt="alt">
          <div v-else class="not-poster">
              <p>{{ originalTitle}}</p>
          </div>
      </div>
      <!-- /card poster -->
      <!-- card info hidden, showed on hover -->
      <div class="info">
            <h2 class="title"><b>Titolo: </b> {{ title }}</h2>
            <h3 class="org_title"><b>Titolo originale: </b> {{ originalTitle }}</h3>
            <div class="flag">
                <country-flag v-if="isAvailable()" :country='getFlags(language)' size='small' shadow class="lang"/>
                <span v-else>{{ language }}</span>
            </div>
            <div class="vote">
            <font-awesome-icon v-for="(item, index) in votes"
                :key="index" :icon="[votesArray(index, vote), 'star']" class="star" /> 
            </div>
            <p><b>Overview: </b>{{ overview }}</p>
        </div>
      <!-- /card info hidden, showed on hover -->
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
            // api request data
            queryLink: 'https://api.themoviedb.org/3/search/',
            apiKey: '981731b128a2c3353bf07ea0418b25f5', //mia api_key
            lang: 'it-IT',
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
        },
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
        },
        isHover() {
            
        }
    }
}
</script>

<style lang="scss">
@import '../assets/scss/partials/_mixins.scss';

.card {
    margin: 1em;
    flex-basis: 22%;
    text-align: center;
    position: relative;
    .poster {
        height: 70vh;
        border: 1px solid white;
        img {
            width: 100%;
            height: 100%;
        }
        .not-poster {
            height: 100%;
            line-height: 100%;
            text-align: center;
            color: white;
            font-size: 1em;
            p {
            vertical-align: middle;
            }
        }
    }
    &:hover .poster {
        display: none;
    }
    .info {
        display: none;
        @include absolute(0, 0);
        background-color: black;
        width: 100%;
        height: 70vh;
        color: white;
        text-align: start;
        padding: .5em;
        overflow: auto;
        h2,
        h3,
        p,
        .flag span,
        .star {
            margin: .5em;
        }
        h2,
        h3,
        p {
            font-size: 1em;
            font-weight: 300;
        }
        .star {
            color: rgb(255, 208, 0);
        }
    }
    &:hover .info {
        display: block;
    }
}
</style>