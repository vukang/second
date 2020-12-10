<template>
  <div class="mainDisplay">
    <div id="instr">
      Instructions: Hero & Vill need EXACTLY 2 cards | Board needs min. 3 board
      cards
    </div>
    <Villain-panel
      :villainC="villainC"
      :results="results"
      :resetV="resetV"
      :setVill="setVill"
      :rndCards="genRndNSplice"
    ></Villain-panel>
    <Board
      :community="dataCommunityCards"
      :resetB="resetB"
      :setBoard="setBoard"
      :rndCards="genRndNSplice"
    ></Board>
    <PlayerPanel
      :data="heroC"
      :sendFunktion="sendFunktion"
      :results="results"
      :resetH="resetH"
      :rndCards="genRndNSplice"
      :setHero="setHero"
    ></PlayerPanel>
  </div>
</template>

<script>
import Board from "./Board.vue";
import PlayerPanel from "./PlayerPanel.vue";
import VillainPanel from "./VillainPanel.vue";

export default {
  props: [
    "heroC",
    "dataCommunityCards",
    "sendFunktion",
    "results",
    "villainC",
    "resetB",
    "resetH",
    "resetV",
    "genRndNSplice",
    "setHero",
    "setVill",
    "setBoard",
  ],
  components: {
    Board,
    PlayerPanel,
    VillainPanel,
  },
  data() {
    return {};
  },
  computed: {},
};
</script>

<style scoped>
.mainDisplay {
  width: 80%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  /* justify-items: center; */
}

#instr {
  border-bottom: 2px dotted black;
  padding-bottom: 2px;
}
</style>