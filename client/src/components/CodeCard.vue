<template>
  <section>

    <article v-for="result in searchResults" :key="result.name">
      {{ result.name }} <br/>
      {{ result.description }}
    </article>

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