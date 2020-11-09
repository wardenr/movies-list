<template>
  <div id="genre-list">
    <div v-for="[genre, titlesList, index] in Object.entries(filteredMoviesByGenre)" :key="index">
      <p> {{ genre }} </p>
      <ol>
        <li v-for="(title, index) in titlesList" :key="index"> {{ title }} </li>
      </ol>
    </div>
  </div>
</template>

<script>
import flow from 'lodash/fp/flow'
import filter from 'lodash/fp/filter'
import transform from 'lodash/fp/transform'

export default {
  name: 'ListMoviesByGenre',
  props: {
    movies: Array
  },
  computed: {
    filteredMoviesByGenre() {
      const rangeBegin = Math.floor(Math.random() * (this.movies.length - 100));
      const moviesListSlice = this.movies.slice(rangeBegin, rangeBegin + 100);

      return flow(
        filter(movie => movie.genres.length),
        transform((accumulative, movie) => {
          movie.genres.forEach(genre => {
            if (!accumulative[genre]) {
              accumulative[genre] = [];
            }

            accumulative[genre].push(movie.title);
        })}, {})
      )(moviesListSlice);
  }
 }   
}
</script>

<style scoped>
</style>
