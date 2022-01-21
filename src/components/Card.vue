<template>
  <div class="card">
        {{ title }}
        {{ originalTitle }}
        <country-flag :country='getFlags(language)' size='small' shadow />
        <i class="far fa-star"></i>
        <i class="fas fa-star"></i>
        <!-- <font-awesome-icon icon="user-secret" /> -->
        <!-- <font-awesome-icon icon="'star'" /> -->
        <font-awesome-icon :icon="['far', 'star']" />
        <font-awesome-icon :icon="['fas', 'star']" />
        {{ vote }}
        <img :src="poster" :alt="alt">
  </div>
</template>

<script>




export default {
    name: 'Card',
    compontent: {

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
        }
    }
}
</script>

<style>

</style>