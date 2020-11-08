<template>
  <div id="genre-list">
    <div v-for="(genreEntry, index) in filteredMoviesByGenre" :key="index">
      <p> {{ genreEntry[0] }} </p>
      <ol>
        <li v-for="(title, index) in genreEntry[1]" :key="index"> {{ title }} </li>
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
  name: 'MoviesListByGenre',
  props: {
    movies: Array
  },
  data: () => ({
  }),
  computed: {
    filteredMoviesByGenre() {
      let movieListSlice = this.movies.slice(0, 100);

      let genreList = flow(
        map(movie => movie.genres),
        flatten,
        uniq,
        map(genre => [genre, []]),
        fromPairs
      )(movieListSlice);

      for (const [genre, movieTitles] of Object.entries(genreList)) {
        let foundMovieTitles = flow(
          filter(movie => movie.genres.includes(genre)),
          map(movie => movie.title)
        )(movieListSlice);

        movieTitles.push(...foundMovieTitles);
        console.log(movieTitles);
      }

      console.log(genreList);
      return _.toPairs(genreList);
    }
  },
  methods: {
  }
}
</script>

<style scoped>
</style>
