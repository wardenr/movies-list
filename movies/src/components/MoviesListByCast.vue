<template>
  <div id="cast-list">
    <div v-for="(castEntry, index) in filteredMoviesByCast" :key="index">
      <p> {{ castEntry[0] }} </p>
      <ol>
        <li v-for="(title, index) in castEntry[1]" :key="index"> {{ title }} </li>
      </ol>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import flow from 'lodash/fp/flow'
import map from 'lodash/fp/map'
import uniq from 'lodash/fp/uniq'
import flatten from 'lodash/fp/flatten'
import filter from 'lodash/fp/filter'
import fromPairs from 'lodash/fp/fromPairs'

export default {
  name: 'MoviesListByCast',
  props: {
    movies: Array
  },
  data: () => ({
  }),
  computed: {
    filteredMoviesByCast() {
      let movieListSlice = this.movies.slice(0, 100);

      let castList = flow(
        map(movie => movie.cast),
        flatten,
        uniq,
        map(cast => [cast, []]),
        fromPairs
      )(movieListSlice);

      for (const [cast, movieTitles] of Object.entries(castList)) {
        let foundMovieTitles = flow(
          filter(movie => movie.cast.includes(cast)),
          map(movie => movie.title)
        )(movieListSlice);

        movieTitles.push(...foundMovieTitles);
        console.log(movieTitles);
      }

      console.log(castList);
      return _.toPairs(castList);
    }
  },
  methods: {
  }
}
</script>

<style scoped>
</style>
