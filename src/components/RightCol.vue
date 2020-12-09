<template>
  <div class="mainDisplay">
    <div id="instr">
      Instructions: 1) Pick Hero cards 2) Pick villain cards 3) Pick at least 3
      board cards
    </div>
    <Villain-panel :villainC="villainC" :results="results"></Villain-panel>
    <Board :community="dataCommunityCards"></Board>
    <PlayerPanel
      :data="dataHoleC"
      :sendFunktion="sendFunktion"
      :results="results"
    ></PlayerPanel>
    
  </div>
</template>

<script>
import Board from "./Board.vue";
import PlayerPanel from "./PlayerPanel.vue";
import VillainPanel from "./VillainPanel.vue";

export default {
  props: [
    "selected",
    "getHole",
    "dataHoleC",
    "dataCommunityCards",
    "sendFunktion",
    "results",
    "villainC",
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
}
</style>