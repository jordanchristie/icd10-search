<template>
  <div>
    <form v-if="( searchMethod = 'Term' )">
      <input type="text" v-on:change="handleInput" placeholder="Search by term" />
      <input type="submit" value="Submit" @click="searchByTerms" />
    </form>
    <form v-else>
      <input type="text" v-model="code" placeholder="Search by code" />
      <input type="submit" value="Submit" @click="searchByCode" />
    </form>
    <p>{{ searchTerm }}</p>
  </div>
</template>

<script>
export default {
  name: "CodeSearch",
  props: {
    searchMethod: String,
    searchTerm: String,
    code: String
  },
  data() {
    return {
      
    };
  },
  methods: {
    handleInput(e) {
      return this.$emit('update', e.target.value)
    },
    async searchByTerms(e) {
      e.preventDefault();
      const res = await fetch(`http://www.icd10api.com/?code=${this.searchTerm}&desc=long`);
      //const res = await fetch(`https://clinicaltables.nlm.nih.gov/api/icd10cm/v3/search?sf=code&terms=${this.searchTerm}`)
      const json = await res.json();

      console.log(json);
    },
    async searchByCode(e) {
      e.preventDefault();
      const res = await fetch(`http://www.icd10api.com/?code=${this.code}&desc=long`);
      //const res = await fetch(`https://clinicaltables.nlm.nih.gov/api/icd10cm/v3/search?sf=code&terms=${this.searchTerm}`)
      const json = await res.json();

      console.log(json);
    }
  }
};
</script>

<style>

</style>