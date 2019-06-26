<template lang="html">

  <select v-on:change="handleSelect" v-model="selected">
    <option disabled value="">Please select one</option>
    <option v-for="(country, index) in countries" :value="index">{{country.name}}</option>
  </select>



</template>

<script>

import { eventBus} from '../main.js'

export default {
  name: "country-select",
  data(){
    return{
      selected: null,
    }
  },
  props: ['countries'],
  methods: {
    handleSelect(){
      eventBus.$emit('country-selected', this.selected);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
