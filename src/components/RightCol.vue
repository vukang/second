<template>
  <div class="mainDisplay">
    <Board :community="dataCommunityCards"></Board>
    <PlayerPanel
      :data="dataHoleC"
      :sendFunktion="sendFunktion"
      :results="results"
    ></PlayerPanel>
    <Villain-panel :villainC="villainC"></Villain-panel>
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
}
</style>