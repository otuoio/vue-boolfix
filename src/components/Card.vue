<template>
  <div class="card">
        {{ title }}
        {{ originalTitle }}
        <country-flag :country='getFlags(language)' size='small' shadow />
        {{ vote }}
        <img :src="poster" :alt="alt">
  </div>
</template>

<script>
export default {
    name: 'Card',
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