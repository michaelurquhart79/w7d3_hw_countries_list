<template lang="html">
  <div>
    <h1>Countries</h1>
    <div class="main-container">
      <!-- <countries-list :countries='countries'></countries-list> -->
      <country-select :countries='countries'></country-select>
      <country-detail :country='selectedCountry'></country-detail>
    </div>
  </div>
</template>

<script>
// import CountriesList from './components/CountriesList.vue'
import CountrySelect from './components/CountrySelect.vue'
import CountryDetail from './components/CountryDetail.vue'
import {eventBus} from './main.js'

export default {
  name: 'app',
  data(){
    return{
      countries: [],
      selectedCountry: null
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (countryIndex) => {
      this.selectedCountry = this.countries[countryIndex];
    })

  },
  components: {
    // "countries-list": CountriesList,
    "country-select": CountrySelect,
    "country-detail": CountryDetail
  }
}
</script>

<style>
  .main-container{
    display: flex;
    justify-content: space-between;
  }
</style>
