<template>
  <div id="app">
    <MoviesFilm />
  </div>
</template>

<script>
import MoviesFilm from './components/MainMovies.vue'

export default {
  name: 'App',
  components: {
    MoviesFilm,
  }
}
</script>

<style lang="scss">

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
