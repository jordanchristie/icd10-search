<template>
  <div>
    <form v-if="termSearch">
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

  </div>
</template>

<script>
export default {
  name: "CodeSearch",
  props: {
    termSearch: Boolean
  },
  data() {
    return {
      term: " ",
      code: " "
    };
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
      }));

      this.$emit("getSearchResults", formattedData);
    },
    async searchByCode(e) {
      e.preventDefault();
      const res = await fetch(`http://www.icd10api.com/?code=${this.code}&desc=long&r=json`);

      const data = await res.json();

      const formattedData = {
        name: data.Name,
        description: data.Description
      };

      return this.$emit("getSearchResults", formattedData);
    }
  }
};
</script>

<style>
  input[type=text] {
    width: 60%;
    font-size: 24px;
    border: none;
    border-bottom: 1px solid #333;
    outline: none;
    padding-top: 10px;
  }
</style>