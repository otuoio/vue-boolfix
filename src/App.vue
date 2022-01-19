<template>
  <div id="app">
    <Header @compileInfo="setMovie($event)"/>
    <Main 
    :movieFind="movieSearch"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
  name: "App",
  components: {
    Header,
    Main
  },
  data() {
    return {
      movieSearch: [],
    }
  },
  methods: {
    setMovie(array) {{
      this.movieSearch = array;
    }}
  }
};
</script>

<style lang="scss">
</style>
