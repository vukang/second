<template>
  <div class="villainContainer">
    <h3>Villain #1</h3>
    <div class="villCards" v-for="(vC, index) in villainC" :key="index">
      {{ vC }}
    </div>
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
  height: 120px;
  background-color: azure;
}

.villCards {
  display: inline;
}
</style>