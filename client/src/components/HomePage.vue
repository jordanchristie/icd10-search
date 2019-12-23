<template>
  <div class="home-page">
  <h1>I am teh VUE</h1>
  <button @click="handleSearchChange">Search by {{searchBy}}</button>
  <code-search :searchMethod="searchBy" @update:="searchTerm" />
  </div>
</template>

<script>
import CodeSearch  from './CodeSearch';

export default {
  components: {
    CodeSearch
  },
  data() {
    return {
      searchBy: "Term",
      searchTerm: "",
      code: ""
    }
  },
  methods: {
    handleSearchChange() {
      this.searchBy = this.searchBy == 'Term' ? 'Code' : 'Term' 
    }
  }
};
</script>

<style>

</style>