<template>
  <div class="home-page">
    <h1>ICD-10 Code Finder</h1>
    <button @click="handleSearchChange">Search by {{ searchMethod }}</button>
    <code-search 
      :searchMethod="searchMethod"
      @getSearchResults="getSearchResults" />
    <code-card 
      :searchResults="searchResults" 
      />
  </div>
</template>

<script>
import CodeSearch from "./CodeSearch";
import CodeCard from "./CodeCard";

export default {
  components: {
    CodeSearch,
    CodeCard
  },
  data() {
    return {
      searchMethod: "Term",
      searchResults: []
    };
  },
  methods: {
    handleSearchChange() {
      this.searchMethod = this.searchMethod == "Term" ? "Code" : "Term";
    },
    getSearchResults(codes) {
      console.log(codes)
      this.searchResults = codes
    }
  }
};
</script>

<style>

</style>