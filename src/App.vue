<template>
  <div id="app">
    <div id="layout">
      <LeftCol :setSelected="setSelected" :setHole="setHole" 
      :setH="setHoleCards" :setC="setCommunityCards" :setV="setVillainCards" :resetAll="resetAll"
      />
      <RightCol
        :sendFunktion="sendData"
        :selected="getSelected"
        :getHole="getHoleCards"
        :dataHoleC="this.holeCards"
        :dataCommunityCards="this.communityCards"
        :villainC="this.villainCards"
        :results="this.returnedData"
        :key="Math.random()"
        :key2="Math.random()"
      />
    </div>
  </div>
</template>

<script>
import LeftCol from "./components/LeftCol.vue";
import RightCol from "./components/RightCol.vue";

export default {
  name: "App",
  components: {
    LeftCol,
    RightCol,
  },
  data() {
    return {
      selectedCards: [{}, {}],
      holeCards: [],
      villainCards: [],
      communityCards: [],
      returnedData: [],

      heroC: [],
      villC: [],
      boardC: [],
    };
  },
  methods: {
    sendData() {
      const meinRequest = new Request("http://localhost:9999/sendData", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify({
          selectedCards: this.selectedCards,
          holeCards: this.holeCards,
          villainCards: this.villainCards,
          communityCards: this.communityCards,
        }),
      });

      fetch(meinRequest)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          return (this.returnedData = data);
        });
    },

    resetAll() {
      this.selectedCards= [{}, {}];
      this.holeCards= [];
      this.villainCards= [];
      this.communityCards = [];


      this.heroC= [];
      this.villC= [];
      this.boardC= [];

      window.location.reload()
    },

    setHoleCards(karte) {
      console.log(karte)

      if (!this.holeCards.includes(karte) &&  this.holeCards.length < 2 && !this.villainCards.includes(karte) && !this.communityCards.includes(karte)) {
          console.log('in here...H')
          this.heroC.push(karte);
          this.holeCards.push(karte);
      }

      if (this.holeCards.length >= 2) {
        console.log(this.holeCards);
        console.log("Hero cant have more cards...")
        } 
    },

    setCommunityCards(karte) {
      console.log(karte)

      if (!this.communityCards.includes(karte) && this.communityCards.length < 5 && !this.holeCards.includes(karte) && !this.villainCards.includes(karte)) {
        console.log('in here...C')
        this.boardC.push(karte);
        this.communityCards.push(karte);
      }
    },

    setVillainCards(karte) {
      console.log(karte)

      if (!this.villainCards.includes(karte) && this.villainCards.length < 2 && !this.holeCards.includes(karte) && !this.communityCards.includes(karte)){
        console.log('in here...V')
        this.villC.push(karte);
        this.villainCards.push(karte);
      }
    },

    setSelected(card) {
      for (let key in card) {
        // console.log(key, card);
        // console.log(this.selectedCards[0].card);
        // console.log(this.selectedCards[1].card);

        if (
          this.selectedCards[0].card != undefined &&
          this.selectedCards[1].card == undefined
        ) {
          this.selectedCards[1][key] = card[key];
        }

        this.selectedCards[0][key] = card[key];

        /* 
        if (this.selectedCards[0].length !== 0) {
          this.selectedCards[0][key] = card[key];
        } else {
          this.selectedCards[1][key] = card[key];
        } */

        // this.selectedCards[0][key] = card[key];

        this.$forceUpdate();
      }
    },

     setHole(textContent) {
      textContent = textContent.trim();

      if (this.holeCards.length >= 2) {
        console.log(this.holeCards);
        console.log("adding to villain's cards here...");
        this.setVillainHole(textContent);
      }

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
    },

    pushToCommunityCards(textContent) {
      console.log(this.communityCards);

      console.log(this.communityCards.includes(textContent));

      if (this.communityCards.includes(textContent)) {
        console.log("need deletion!");
        if (this.communityCards.length == 1) {
          console.log("only one !");
          return (this.communityCards.length = 0);
        } else {
          console.log("filtering the rest...");
          let filtered = this.communityCards.filter((el) => el != textContent);
          console.log(filtered);
          this.communityCards = filtered;
          console.log(this.communityCards);

          return (this.communityCards = filtered);
        }
      }

      if (
        this.communityCards.length < 5 &&
        !this.communityCards.includes(textContent)
      ) {
        this.communityCards.push(textContent);
      }
    },

    setVillainHole(textContent) {
      textContent = textContent.trim();

      if (this.villainCards.length >= 2) {
        console.log(this.villainCards);
        console.log("adding to community cards here...");
        this.pushToCommunityCards(textContent);
      }

      if (
        !this.villainCards.includes(textContent) &&
        this.villainCards.length <= 1
      ) {
        console.log("push to arr");
        this.villainCards.push(textContent);
      } else if (this.villainCards.length <= 1) {
        console.log("pop if 1");
        this.villainCards.pop();
      } else {
        let filtered = this.villainCards.filter((el) => el != textContent);
        console.log(filtered);
        this.villainCards = filtered;
      }
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

<style scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

#layout {
  display: flex;
}
</style>
