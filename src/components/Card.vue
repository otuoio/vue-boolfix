<template>
  <div class="card">
        {{ title }}
        {{ originalTitle }}
        {{ language }}
        {{ vote }}
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
    }
}
</script>

<style>

</style>