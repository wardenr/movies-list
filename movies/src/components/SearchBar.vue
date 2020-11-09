<template>
  <div id="search-bar">
    <form>
      <div class="form-group">
          <label for=inputTitle>Tytuł</label>
          <input type="text" id=inputTitle class="form-control" placeholder="Podaj tytuł lub fragment tytułu filmu" v-model="title" />
      </div>
      <div class="form-group row">
        <label class="col-sm-4 col-form-label" for="inputProductionFrom">Rok produkcji od:</label>
        <div class="col-sm-8">
            <input type="text" id=inputProductionFrom class="form-control"  placeholder="Liczba naturalna z przedziału 1900-2019" v-model="productionFrom" />
        </div>
      </div>
      <div class="form-group row">
          <label class="col-sm-4 col-form-label" for="inputProductionTo">Rok produkcji do:</label>
          <div class="col-sm-8">
              <input type="text" id=inputProductionTo class="form-control" placeholder="Liczba naturalna z przedziału 1900-2019" v-model="productionTo" />
          </div>
      </div>
      <div class="form-group">
        <label for="inputCast">Obsada</label>
        <input type="text" id="inputCast" class="form-control" placeholder="Imię i nazwisko" v-model="cast" />
      </div>
      <div class="form-group row">
          <input type="button" class="btn btn-info col-sm-12" value="Szukaj" v-on:click="fetchSearchCriteria"/>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data: () =>  ({
    title: "",
    productionFrom: 1900,
    productionTo: 2019,
    cast: ""
  }),
  methods: {
    fetchSearchCriteria() {
      this.$emit('updateSearchCriteriaEvent', {
        title: this.title,
        productionFrom: this.productionFrom, 
        productionTo: this.productionTo,
        cast: this.cast
      });
    }
  }
}
</script>

<style scoped>
</style>
