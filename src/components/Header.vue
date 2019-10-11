<template>
  <div>
    <b-nav>
      <b-nav-item disabled>Computer science Quiz</b-nav-item>
      <b-nav-item disabled>Score:</b-nav-item>
      <b-nav-item disabled>{{p}}/10</b-nav-item>
    </b-nav>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      score: 0
    };
  },
  props: {
    p: Number
  }
};
</script>

<style scoped>
</style>