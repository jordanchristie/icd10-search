<template>
  <div>
    <form v-if="searchMethod == 'Term'">
      <input 
        type="text" 
        v-model="term" 
        placeholder="Search by term" />
      <input 
        type="submit" 
        value="Submit" 
        @click="searchByTerms" />
    </form>

    <form v-else>
      <input 
        type="text" 
        v-model="code" 
        placeholder="Search by code" />
      <input 
        type="submit" 
        value="Submit" 
        @click="searchByCode" />
    </form>

    <p>Search results for: {{ code }}</p>
  </div>
</template>

<script>
export default {
  name: "CodeSearch",
  props: {
    searchMethod: String
  },
  data() {
    return {
      term: '',
      code: ''
    }
  },
  methods: {
    async searchByTerms(e) {
      e.preventDefault();

      const res = await fetch(`https://clinicaltables.nlm.nih.gov/api/icd10cm/v3/search?sf=code,name&terms=${this.term}`)
      // const res = await fetch('https://clinicaltables.nlm.nih.gov/api/icd10cm/v3/search?sf=code,name&terms=tuberc')
      const data = await res.json();

      const formattedData = await data[3].map(code => ({
        name: code[0],
        description: code[1]
      }))

      this.$emit('getSearchResults', formattedData);
    },
    async searchByCode(e) {
      e.preventDefault();
      const res = await fetch(`http://www.icd10api.com/?code=${this.code}&desc=long&r=json`);
  
      const data = await res.json();

      const formattedData = {
        name: data.Name,
        description: data.Description
      }

      return this.$emit('getSearchResults', formattedData);
    }
  }
};
</script>

<style>

</style>