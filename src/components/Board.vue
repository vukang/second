<template>
  <div id="cardsContainer">
    <h4>Community Cards</h4>
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
</style>