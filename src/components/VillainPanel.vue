<template>
  <div class="villainContainer">
    <h4><div id="rndBtn" @click="rndV()">🎲</div> Villain #1 <div id="resBtn" @click="delH()">❌</div></h4>
    <div class="villCards" v-for="(vC, index) in villainC" :key="index">
      {{ vC.value }}
    </div>
    <div class="results">Win: {{ resV }}</div>
  </div>
</template>

<script>
export default {
  props: ["villainC", "results"],
  data() {
    return {
      resV: this.results.length?this.results[1].slice(25) : false,
    };
  },
  methods: {
    delH() {
      console.log("delete V cards in data array!")
    },
    rndV(){
      console.log("rnd c 4 vill")
    }
  }

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

#rndBtn {
  display: inline;
  cursor: pointer;
}

#resBtn {
  display: inline;
  width: 15px;
  height: 15px;
  cursor: pointer;
}
</style>