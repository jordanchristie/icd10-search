<template>
  <div class="home-page">
    <h1>ICD-10 Code Finder</h1>
    <button @click="handleSearchChange">Search by {{searchMethod}}</button>
    <code-search :searchMethod="searchMethod"/>
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
      searchMethod: "Term"
    }
  },
  methods: {
    handleSearchChange() {
      this.searchMethod = this.searchMethod == 'Term' ? 'Code' : 'Term' 
    }
  }
};
</script>

<style>

</style>