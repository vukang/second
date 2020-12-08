<template>
  <div class="villainContainer">
    <h3>Villain #1</h3>
    {{ villainC }}
    <div class="results">Win: {{ resV }}</div>
  </div>
</template>

<script>
export default {
  props: ["villainC", "results"],
  data() {
    return {
      resV: this.results[1].slice(25),
    };
  },
  methods: {},
  computed: {},
};
</script>

<style scoped>
.villainContainer {
  width: 200px;
  height: 100px;
  background-color: azure;
}
</style>