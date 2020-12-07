<template>
  <div class="mainDisplay">
    Main...

    <p v-for="(card, index) in selected" :key="index">
      {{ card }}
    </p>
    <p>
      {{ ~~(Math.random() * 100) }}
    </p>
    <p v-for="(holeCard, index) in getHole" :key="index" id="player1">
      {{ holeCard }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["selected", "getHole"],
};
</script>

<style scoped>
.mainDisplay {
  width: 80%;
  height: 100vh;
}

#player1 {
  display: inline;
}
</style>