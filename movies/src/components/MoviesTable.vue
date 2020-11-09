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
      <input type="button" value="Show more entries" v-on:click="appendMoviesTableEntriesAmount" class="btn btn-primary" v-if="currentRowsAmount < movies.length">
  </div>
</template>

<script>
export default {
  name: 'MoviesTable',
  props: {
    movies: Array
  },
  data: () => ({
    currentRowsAmount: 10,
  }),
  computed: {
    currentEntries() {
      return this.movies.slice(0, this.currentRowsAmount);
    }
  },
  methods: {
    appendMoviesTableEntriesAmount() {
      const totalEntriesAmount = this.movies.length;

      this.currentRowsAmount += 10;

      if (this.currentRowsAmount > totalEntriesAmount) {
        this.currentRowsAmount = totalEntriesAmount;
      }

      this.currentEntries = this.movies.slice(0, this.currentRowsAmount);
    }
  }
}
</script>

<style scoped>
</style>
