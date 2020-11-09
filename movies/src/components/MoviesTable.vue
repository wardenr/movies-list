<template>
  <div id="movies-table">
      <table class="table-condensed table-hover">
        <thead>
          <tr>
            <th>Title</th>
            <th>Production Year</th>
            <th>Cast</th>
            <th>Genres</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(movie, index) in currentEntries" :key="index">
            <td>{{movie.title}}</td>
            <td>{{movie.year}}</td>
            <td>{{movie.cast.join()}}</td>
            <td>{{movie.genres.join()}}</td>
          </tr>
        </tbody>
      </table>
      <input type="button" value="Show more entries" v-on:click="appendMoviesTableEntriesAmount" class="btn btn-primary" v-if="currentRowsAmount < currentMoviesList.length">
  </div>
</template>

<script>
import _ from 'lodash';

export default {
  name: 'MoviesTable',
  props: {
    movies: Array,
    searchCriteria: Object
  },
  data: () => ({
    currentRowsAmount: 10,
    currentMoviesList: []
  }),
  created() {
    this.currentMoviesList = this.movies;
  },
  computed: {
    currentEntries() {
      return this.currentMoviesList.slice(0, this.currentRowsAmount);
    }
  },
  methods: {
    appendMoviesTableEntriesAmount() {
      const totalEntriesAmount = this.currentMoviesList.length;

      this.currentRowsAmount += 10;

      if (this.currentRowsAmount > totalEntriesAmount) {
        this.currentRowsAmount = totalEntriesAmount;
      }

      this.currentEntries = this.currentMoviesList.slice(0, this.currentRowsAmount);
    }
  },
  watch: {
    searchCriteria() {
      this.currentMoviesList = _.filter(this.movies, movie => {
        return movie.title.includes(this.searchCriteria.title) &&
               (movie.year >= this.searchCriteria.productionFrom) &&
               (movie.year <= this.searchCriteria.productionTo) &&
               (!this.searchCriteria.cast || movie.cast.includes(this.searchCriteria.cast));
      });

      this.currentRowsAmount = 10;
    }
  },
}
</script>

<style scoped>
</style>
