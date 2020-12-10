<template>
  <div class="cardsContainer">
    Pick your cards...
    <div class="columnCardContainer">
      <CardsCol 
      :heroC="heroC"
      :villC="villC"
      :boardC="boardC"
      :setH="setH"
      :setC="setC" 
      :setV="setV" 
      :resetAll="resetAll" 
      :kopiereKarte="kopiereKarte" 
      :kartenstapel="kartenstapel"
      >
       </CardsCol>
    </div>
  </div>
</template>



<script>
import CardsCol from "./CardsCol.vue";
export default {
  props: [ "heroC" ,"villC" ,"boardC" ,"setH", "setC", "setV", "resetAll", 'kopiereKarte', 'kartenstapel'],
  components: {
    CardsCol,
  },
};
</script>

<style scoped>
.cardsContainer {
  box-sizing: border-box;
  width: 220px;
  height: 100vh;
}
</style>