<template>
  <div class="card">
      <h2 class="title">Title: {{ title }}</h2>
      <h3 class="org_title">Original Title: {{ originalTitle }}</h3>
      <div class="flag">
          Language: <country-flag :country='getFlags(language)' size='small' shadow />
      </div>
      <div class="vote">
            Vote: <font-awesome-icon v-for="(item, index) in votes"
            :key="index" :icon="[votesArray(index, vote), 'star']" /> 
      </div>
      <div class="poster">
          <img :src="poster" :alt="alt">
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
        }
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
    
</style>