<template>
  <div id="app">
    <MoviesListByCast :movies="moviesList"/>
  </div>
</template>

<script>
    //<MoviesTable :movies="moviesList"/>
import json from './assets/movies.json'
//import SearchBar from './components/SearchBar.vue'
//import MoviesTable from './components/MoviesTable.vue'
import MoviesListByCast from './components/MoviesListByCast.vue'
//import MoviesListByGenre from './components/MoviesListByGenre.vue'

export default {
  name: 'App',
  data: () => ({
    moviesList: json.valueOf()
  }),
  components: {
 //   SearchBar
    MoviesTable,
//    MoviesListByCast,
 //   MoviesListByGenre
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
