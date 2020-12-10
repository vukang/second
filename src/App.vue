<template>
  <div id="app">
    <div id="layout">
      <LeftCol 
      :heroC="heroC"
      :villC="villC"
      :boardC="boardC"
      :setH="setHoleCards"
      :setC="setCommunityCards"
      :setV="setVillainCards"
      :resetAll="resetAll"
      :kopiereKarte="kopiereKarte"
      :kartenstapel="kartenstapel"
      
      />
      <RightCol
        :sendFunktion="sendData"
        :heroC="heroC"
        :dataCommunityCards="boardC"
        :villainC="villC"
        :results="returnedData"
        :resetB="resetBoard"
        :resetH="resetHero"
        :resetV="resetVil"
        :genRndNSplice="generateRandomAndSplice"
        :setHero="setHero"
        :setVill="setVill"
        :setBoard="setBoard"
        :key="Math.random()"
        :key2="Math.random()"
      />
    </div>

    <!-- {{ generateRandomAndSplice()  }} -->
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

      returnedData: [],

      heroC: [],
      villC: [],
      boardC: [],

      kartenstapel: this.kartenstapelErzeugen(),
      // bereinigterStapel: this.aktuellerStapel

    }
  },
  methods: {
    // POST req
    sendData() {
      const meinRequest = new Request("http://localhost:9999/sendData", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify({

          heroCards: this.heroC,
          villainCards: this.villC,
          communityCards: this.boardC,
        }),
      });

      fetch(meinRequest)
        .then((response) => response.json())
        .then((data) => {
          // console.log(data);
          return (this.returnedData = data);
        });
    },

    kopiereKarte(karte, target, maxLength=2){

      if (this.heroC.includes(karte) || this.villC.includes(karte) || this.boardC.includes(karte) ) {
        console.error(("Can't copy card, because already in use!"))
        throw Error("Card already in use!")
      } else {
        if (this[target].length < maxLength)
        {this[target].push(karte)}
      }
     

      
    },

    kartenstapelErzeugen() {
      let cards = 'A23456789TJQK'.split('');
      let suits = ['♣️', '♦️', '♥️', '♠️'];
      let kStapel = [];

      cards.forEach((card) => {
        suits.forEach((suit) => {
        kStapel.push({ card, suit, value: card + suit });
        });
      });
      return kStapel;
    },

    // reset&del methods
    resetAll() {
      
      this.heroC= [];
      this.villC= [];
      this.boardC= [];

      console.log("Resetted cards")
      // window.location.reload()
    },

    resetHero(){
      this.heroC = [];
    },

    resetVil(){
      this.villC = [];
    },

    resetBoard(){
      this.boardC = [];
    },

    // alte methoden /////////////
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
    ///////////////

    setHero(cardArray){
      this.heroC = cardArray
    },

    setVill(cardArray){
      this.villC = cardArray
    },

    setBoard(cardArray){
      this.boardC = cardArray
    },


    generateRandomAndSplice (num = 2,) {

      let cleanStapel = this.aktuellerStapel

      num = Math.min(num, cleanStapel.length);


      let leeresArr = [];

      while (leeresArr.length < num) {
        let rndNum = ~~(Math.random() * cleanStapel.length);

        leeresArr.push(cleanStapel.splice(rndNum, 1)[0]);
      }

      return leeresArr; 
    },
  
 
},  computed: {

    aktuellerStapel : function() {
      let bereinigt = this.kartenstapel.filter((karte) => {
        return !this.heroC.some((heroKarte)=> heroKarte == karte)
      })
      bereinigt = bereinigt.filter((karte) => {
        return !this.villC.some((villKarte)=> villKarte == karte)
      })
      bereinigt = bereinigt.filter((karte) => {
        return !this.boardC.some((boardKarte)=> boardKarte == karte)
      })
      return bereinigt
    },


  },
}
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
