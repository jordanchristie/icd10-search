<template>
  <section>
    <transition-group name="fade">
      <article v-for="result in searchResults" :key="result.name">
        <h3>{{ result.name }}</h3>
        <p>{{ result.description }}</p>
      </article>
    </transition-group>
  </section>
</template>

<script>
export default {
  name: "code-card",
  props: {
    searchResults: {
      Name: String,
      Description: String
    }
  },
  data() {
    return {
      index: 0
    };
  }
};
</script>

<style>
section {
  margin: 1em;
  display: flex;
  justify-content: center;
}
article {
  display: flex;
  justify-content: space-around;
}
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s ease-in;
}

.fade-enter,
.fade-leave {
  opacity: 0;
  transform: translateY(50px);
}
</style>
