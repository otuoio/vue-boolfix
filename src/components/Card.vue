<template>
  <div class="card">
        {{ title }}
        {{ originalTitle }}
        {{ language }}
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
    }
}
</script>

<style>

</style>