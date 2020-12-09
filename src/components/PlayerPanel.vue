<template>
  <div id="player">
   <div class="title"> <h4><div id="rndBtn" @click="rndH()">🎲</div> Hero Panel <div id="resBtn" @click="delH()">❌</div></h4>  </div>
    <!-- {{ data }} -->
    <div id="results" v-for="(dat, index) in data" :key="index">
      {{ dat }}
    </div>
    <div class="stats">Win percentage: {{ resHero }}</div>
    <button @click="sendFunktion">Calculate (send to node)</button>
  </div>
</template>

<script>
export default {
  props: ["data", "sendFunktion", "results"],
  data() {
    return {
      resHero: this.results[0].slice(25),
      resVil: this.results[1],
    };
  },
  methods: {
    delH() {
      console.log("delete H cards in data array!")
    },
    rndH(){
      console.log("rnd cards 4 hero")
    }
  }
};
</script>

<style scoped>

.title {
  width: auto;
  height: auto;
  display: flex;
  align-items: center;
  justify-content: center;

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