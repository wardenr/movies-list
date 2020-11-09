<template>
  <div id="app" class="container">
    <h1>Baza filmów</h1>
    <SearchBar />
    <MoviesTable :movies="moviesList"/>
    <h1>Filmy wg obsady</h1>
    <ListMoviesByCast :movies="moviesList" />
    <h1>Filmy wg gatunku</h1>
    <ListMoviesByGenre :movies="moviesList"/>
  </div>
</template>

<script>
import json from './assets/movies.json'
import SearchBar from './components/SearchBar.vue'
import MoviesTable from './components/MoviesTable.vue'
import ListMoviesByCast from './components/ListMoviesByCast.vue'
import ListMoviesByGenre from './components/ListMoviesByGenre.vue'

export default {
  name: 'App',
  data: () => ({
    moviesList: json.valueOf()
  }),
  components: {
    SearchBar,
    MoviesTable,
    ListMoviesByCast,
    ListMoviesByGenre
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
