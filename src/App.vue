<template>
  <div id="app">
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <div id="layout">
      <LeftCol :setSelected="setSelected" :setHole="setHole" />
      <RightCol
        :selected="getSelected"
        :getHole="getHoleCards"
        :key="Math.random()"
        :key2="Math.random()"
      />
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
      holeCards: [],
    };
  },
  methods: {
    setSelected(card) {
      for (let key in card) {
        // console.log(key);
        // console.log(card);
        // console.log(this.selectedCards[0]);
        if (this.selectedCards[0] == undefined) {
          this.selectedCards[0][key] = card[key];
        } else {
          this.selectedCards[1][key] = card[key];
          // console.log(this.selectedCards);
          // console.log(this.selectedCards.length);
          // console.log(this.selectedCards[0]);
          // console.log(this.selectedCards[1]);
          // console.log(this.selectedCards[0].card);
          // console.log(this.selectedCards[1].card);
          // console.log(this.selectedCards.hasOwnProperty());
        }

        this.selectedCards[0][key] = card[key];
        // console.log(key, card);
        // console.log(this.selectedCards);

        this.$forceUpdate();
      }
    },
    setHole(textContent) {
      textContent = textContent.trim();

      if (!this.holeCards.includes(textContent) && this.holeCards.length <= 1) {
        console.log("push to arr");
        this.holeCards.push(textContent);
      } else if (this.holeCards.length <= 1) {
        console.log("pop if 1");
        this.holeCards.pop();
      } else {
        let filtered = this.holeCards.filter((el) => el != textContent);
        console.log(filtered);
        this.holeCards = filtered;
      }

      /* 
      if (this.holeCards.length == 0) {
        this.holeCards.push(textContent);
        console.log("card added to arr");
      } else if (this.holeCards.length == 1) {
        this.holeCards.push(textContent);
        console.log("Second card added to arr");
      } else if (this.holeCards.length > 1) {
        console.log("Players cards are full");
        if (this.holeCards.includes(textContent)) {
          console.log("card needs to be deleted");
          if (this.holeCards.length == 1) {
            this.holeCards.pop();
          } else {
            let filtered = this.holeCards.filter((el) => el != textContent);
            console.log(filtered);
            this.holeCards = filtered;
          }
        }

        console.log("Add to board by default");
      } */
      /* 
      if (this.holeCards.length <= 2)
        if (this.holeCards.length <= 2) {
          this.holeCards.push(textContent);
          console.log("card added to arr");
        } else if (this.holeCards.includes(textContent)) {
          console.log("needs delete");
          this.holeCards.filter((el) => el == !textContent);
          console.log("filtered");
          console.log(this.holeCards);
          // findIndex and splice
        } else if (this.holeCards.length == 2) {
          console.log("Lenght is 2!");
        }
      return this.holeCards; 
*/
    },
  },
  computed: {
    getSelected() {
      return this.selectedCards;
    },
    getHoleCards() {
      return this.holeCards;
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
