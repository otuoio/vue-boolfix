<template>
  <div class="container">
      <ul v-for="(movie, index) in movieFind"
          :key="index">
          <li>
              {{ movie.title || movie.name}}
          </li>
          <li>
              {{ movie.original_title || movie.original_name }}
          </li>
          <li>
              {{ movie.original_language}}
          </li>
          <li>
              {{ movie.vote_average}}
          </li>
      </ul>
  </div>
</template>

<script>

export default {
    name: "Main",
    data() {
        return {

        }
    },
    props: {
        movieFind: {
            type: Array,
        }
    },
    created() {
        
    },
    methods: {
        
    }
}
</script>

<style>

</style>