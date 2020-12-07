<template>
  <div class="cardsContainer">
    Pick your cards...
    <div class="columnCardContainer">
      <CardsCol :setSelected="setSelected" :setHole="setHole"> </CardsCol>
    </div>
  </div>
</template>



<script>
import CardsCol from "./CardsCol.vue";
export default {
  props: ["setSelected", "setHole"],
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