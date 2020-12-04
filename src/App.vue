<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div id="layout">
      <LeftCol :setSelected="setSelected" />
      <RightCol :selected="getSelected" :key="Math.random()" />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import LeftCol from "./components/LeftCol.vue";
import RightCol from "./components/RightCol.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
    LeftCol,
    RightCol,
  },
  data() {
    return {
      selectedCards: [{}, {}],
    };
  },
  methods: {
    setSelected(card) {
      for (let key in card) {
        this.selectedCards[0][key] = card[key];

        this.$forceUpdate();
      }
    },
  },
  computed: {
    getSelected() {
      return this.selectedCards;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#layout {
  display: flex;
}
</style>
