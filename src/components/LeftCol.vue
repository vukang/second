<template>
  <div class="cardsContainer">
    Pick your cards...
    <div class="columnCardContainer">
      <CardsCol :setSelected="setSelected" :setHole="setHole" :setH="setH" :setC="setC" :setV="setV" :resetAll="resetAll"> </CardsCol>
    </div>
  </div>
</template>



<script>
import CardsCol from "./CardsCol.vue";
export default {
  props: ["setSelected", "setHole", "setH", "setC", "setV", "resetAll"],
  components: {
    CardsCol,
  },
};
</script>

<style scoped>
.cardsContainer {
  width: 20%;
  height: 100vh;
}
</style>