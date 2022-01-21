<template>
  <div id="app">
    <Header @compileInfo="setMovie($event)"/>
    <Main 
    :cards="searchArray"
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
    }
  },
  methods: {
    setMovie(array) {{
      this.searchArray = array;
    }}
  }
};
</script>

<style lang="scss">
@import './assets/scss/style.scss';

</style>
