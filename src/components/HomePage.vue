<template>
  <div class="home-page">
    <h1>ICD-10 Code Finder</h1>
    <button @click="toggleSearch">
      Search by {{ termSearch ? "Term" : "Code" }}
    </button>
    <code-search
      :termSearch="termSearch"
      @getSearchResults="getSearchResults"
    />
    <code-card :searchResults="searchResults" />
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
      termSearch: true,
      searchResults: []
    };
  },
  methods: {
    toggleSearch() {
      this.searchResults = [];
      this.termSearch = !this.termSearch;
    },
    getSearchResults(codes) {
      this.searchResults = codes;
    }
  }
};
</script>

<style>
button,
input[type="submit"] {
  font-size: 24px;
  margin: 1em;
  border: 1px solid black;
  border-radius: 5px;
  padding: 15px 20px;
  transition: background 0.3s ease;
}
button:hover,
input[type="submit"]:hover {
  background: #f012be;
  transition: background 0.3s ease;
}
</style>
