<template>
  <section>
    {{ searchResults.Name }} <br/>
    {{ searchResults.Description }}
  </section>
</template>

<script>
export default {
  name: 'code-card',
  props: {
    searchResults: {
      Name: String,
      Description: String
    }
  },
}
</script>

<style>

</style>