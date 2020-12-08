<template>
  <div id="player">
    <h4>Hero Panel</h4>
    <!-- {{ data }} -->
    <div id="results" v-for="(dat, index) in data" :key="index">
      {{ dat }}
    </div>
    <div class="stats">Win percentage: {{ res }}</div>
    <button @click="sendFunktion">Calculate (send to node)</button>
  </div>
</template>

<script>
export default {
  props: ["data", "sendFunktion", "results"],
  data() {
    return {
      res: this.results,
    };
  },
};
</script>

<style scoped>
#results {
  display: inline-block;
}
#player {
  width: 300px;
  height: 150px;
  background-color: darkkhaki;
  border-radius: 10px;
  box-shadow: 12px 12px 2px 1px rgba(164, 164, 166, 0.2);
}
</style>