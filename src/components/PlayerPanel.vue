<template>
  <div id="player">
    <div class="title">
      <h4>
        <div id="rndBtn" @click="rndH()">🎲</div>
        Hero Panel
        <div id="resBtn" @click="delH()">❌</div>
      </h4>
    </div>
    <!-- {{ data }} -->
    <div id="results" v-for="(dat, index) in data" :key="index">
      {{ dat.value }}
    </div>
    <div class="stats">Win: {{ resHero }} {{ entpackt }}</div>
    <button @click="sendFunktion">Calculate (send to node)</button>
  </div>
</template>

<script>
export default {
  props: ["data", "sendFunktion", "results", "resetH", "rndCards", "setHero"],
  data() {
    return {
      resHero: this.results.length ? this.results[0].slice(25) : false,
      resVil: this.results.length ? this.results[1] : false,
      entpackt: this.entpackeResults(),
    };
  },
  methods: {
    delH() {
      console.log("deleting hero's cards in heroC array");
      this.resetH();
    },
    rndH() {
      console.log("Dealing 2 rnd cards to hero");
      this.setHero(this.rndCards(2));
    },

    entpackeResults() {
      console.log(this.results);
      console.log(this.results.status);

      if (this.results.status == "error") {
        console.log("error results...");
        console.log(this.results.messages);
      }

      return this.results.messages;
    },
  },
  computed: {
    res4hero: function () {
      return console.log("in here");
    },
  },
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
  margin: 10px;
}
</style>