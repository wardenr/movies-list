<template>
  <div id="cast-list">
    <div v-for="(entry, index) in filteredMoviesByCast" :key="index">
      <p> {{ entry.name }} </p>
      <ol>
        <li v-for="(title, index) in entry.titles" :key="index"> {{ title }} </li>
      </ol>
    </div>
  </div>
</template>

<script>
import flow from 'lodash/fp/flow'
import map from 'lodash/fp/map'
import uniq from 'lodash/fp/uniq'
import flatten from 'lodash/fp/flatten'
import filter from 'lodash/fp/filter'

export default {
  name: 'MoviesListByCast',
  props: {
    movies: Array
  },
  computed: {
    filteredMoviesByCast() {
      const moviesListSlice = this.movies.slice(0, 100);

      let castList = flow(
        map(movie => movie.cast),
        flatten,
        uniq,
        map(cast => ({ name: cast, titles: [] }))
      )(moviesListSlice);

      for (const entry of castList) {
        entry.titles.push(...flow(
          filter(movie => movie.cast.includes(entry.name)),
          map(movie => movie.title)
        )(moviesListSlice));
      }

      return castList;
    }
  }
}
</script>

<style scoped>
</style>
