<template>
  <div id="cast-list">
    <div v-for="[actorName, titlesList, index] in Object.entries(filteredMoviesByCast)" :key="index">
      <p> {{ actorName }} </p>
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
  name: 'ListMoviesByCast',
  props: {
    movies: Array
  },
  computed: {
    filteredMoviesByCast() {
      const rangeBegin = Math.floor(Math.random() * (this.movies.length - 100));
      const moviesListSlice = this.movies.slice(rangeBegin, rangeBegin + 100);

      return flow(
        filter(movie => movie.cast.length),
        transform((accumulative, movie) => {
          movie.cast.forEach(actorName => {
            if (!accumulative[actorName]) {
              accumulative[actorName] = [];
            }

            accumulative[actorName].push(movie.title);
        })}, {})
      )(moviesListSlice);
  }
 }   
}
</script>
<style scoped>
</style>
