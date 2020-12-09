<template>
  <div id="cardsContainer">
    <h4><div id="rndBtn" @click="rndC()">🎲</div> Community Cards <div id="resBtn" @click="delC()">❌</div></h4>
    <div class="wrapper">
      <!-- {{ community }} -->
      <div
        v-for="(cCard, index) in community"
        :key="index"
        id="indivBoardCards"
      >
        <span id="eachCard"> {{ cCard }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["community"],
  data() {
    return {};
  },
  methods: {
    delC() {
      console.log("delete C cards in data array!")
    },
    rndC(){
      console.log('randomize flop! w/ 3cards')
    }
  }
};
</script>

<style scoped>
#wrapper {
  display: flex;
  flex-direction: row;
}

#indivBoardCards {
  display: inline;
}

#eachCard {
  display: inline;
}

#cardsContainer {
  width: 250px;
  height: 100px;
  background-color: rgb(97, 241, 159);
  border-radius: 100px;
  align-self: center;
  padding-top: 20px;
}


#resBtn {
  display: inline;
  width: 15px;
  height: 15px;
  cursor: pointer;
}

#rndBtn {
  display: inline;
  cursor: pointer;
}

</style>