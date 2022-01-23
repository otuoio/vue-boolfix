<template>
  <div id="app">
    <Header @compileInfo="setMovie($event)"
    @filterGenre="setGenre($event)"/>
    <Main 
    :cards="searchArray"
    :genreFil="filteredGenre"
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
      searchArray: [],
      filteredGenre: ''
    }
  },
  methods: {
    setMovie(array) { //received array emit function
      this.searchArray = array;
    },
    setGenre(text) {
      this.filteredGenre = text;
    }
  }
};
</script>

<style lang="scss">
@import './assets/scss/style.scss';

</style>
