<template>
  <div class="mainDisplay">
    Main...

    <p v-for="(card, index) in selected" :key="index">
      {{ card }}
    </p>
    <p>
      {{ ~~(Math.random() * 100) }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["selected"],
};
</script>

<style scoped>
.mainDisplay {
  width: 80%;
  height: 100vh;
}
</style>