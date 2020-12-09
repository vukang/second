<template>
  <div class="indivCards">
    <div class="cards" v-for="(card, index) in kartenstapel" :key="index">
      <span class="indivCard">
        {{ card.value }}

      <div class="target" @click="(e) => {
        e.currentTarget.parentElement.classList.toggle('active--hero');
        e.currentTarget.parentElement.classList.toggle('indivCard');
        
        // settingH(e, card+suit)
        kopiereKarte(card, 'heroC', 2)
        }">
        H
      </div>

      <div class="target" @click="(e) => {
        e.currentTarget.parentElement.classList.toggle('active--comm');
        e.currentTarget.parentElement.classList.toggle('indivCard');
        
        //settingC(card+suit)
        kopiereKarte(card, 'boardC', 5)}">
        C
      </div>

      <div class="target" @click="(e) =>  {
        e.currentTarget.parentElement.classList.toggle('active--villain');
        e.currentTarget.parentElement.classList.toggle('indivCard');
        
        //settingV(card+suit)}
        kopiereKarte(card, 'villC', 2)}"
        >
        V
      </div>

      </span>
    </div>
    <button @click="reloadPage()" >Reset all</button>
  </div>
</template>

<script>
export default {
  props: ["setSelected", "setHole", "setH", "setC", "setV", 'resetAll', 'kopiereKarte', "kartenstapel", 'boardC'],
  data() {
    return {
      cards: "A23456789TJQK".split(""),
      suits: ["♣️", "♦️", "♥️", "♠️"],


    };
  },
  methods: {
    reloadPage(){
      this.resetAll();
    },

    settingH(e, karte){
      this.setH(karte)
    },

    settingC(karte){
      this.setC(karte)
    },

    settingV(karte){
      this.setV(karte)
    },

    doStuffWhenClicked(karte) {


      this.setHole(karte);
      // console.log(this.communityCards);
    },

    setCard(card, suit) {
      this.setSelected({ card, suit });

      //   let str = `${card}${suit}`;
      //   alert(str);
    },
  },
};
</script>

<style scoped>

.active--villain {
  background-color: red;
  cursor: crosshair;
  border: 1px solid black;

  position: relative;
  display: inline-block;
  width: 50px;
  height: 35px;
  padding: 0px;
  border-right: 1px solid black;
  border-left: 1px solid black;
}

.active--hero {
  background-color: darkkhaki;
  cursor: crosshair;
  border: 1px solid black;

  position: relative;
  display: inline-block;
  width: 50px;
  height: 35px;
  padding: 0px;
  border-right: 1px solid black;
  border-left: 1px solid black;
}

.active--comm {
  background-color: #rgb(97, 241, 159);
  cursor: crosshair;
  border: 1px solid black;

  position: relative;
  display: inline-block;
  width: 50px;
  height: 35px;
  padding: 0px;
  border-right: 1px solid black;
  border-left: 1px solid black;
}

.active {
  background-color: #999;
  cursor: crosshair;

  position: relative;
  display: inline-block;
  width: 25px;
  height: 25px;
  padding: 3px;
  border-right: 1px solid black;
  border-left: 1px solid black;
}

.indivCard {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 35px;
  padding: 0px;
  border-right: 1px solid black;
  border-left: 1px solid black;
  cursor: cell;
}

.cards > span:nth-child(4n) {
  background-color: rgba(36, 216, 39, 0.329);
  color: green;
}

.cards:nth-child(4n) {
  background-color: rgba(36, 216, 39, 0.329);
  color: green;
}



.cards{
  display: inline;
  
}

.indivCard:first-child {
  background-color: rgba(36, 216, 39, 0.329);
  color: green;
}

.indivCard:nth-child(2) {
  background-color: rgba(15, 98, 198, 0.329);
  color: blue;
}
.indivCard:nth-child(3) {
  background-color: rgba(173, 21, 21, 0.329);
  color: indigo;
}
.indivCard:last-child {
  background-color: rgba(127, 127, 127, 0.329);
  color: black;
}

.indivCard:hover {
  border: 1px solid black;
}
.indivCards {
  display: border-box;
}

.target{
  display: none;
  position: absolute;;
  width: 10px;
  height: 10px;
  font-size: 8px;
  right: 0px;

  bottom: 0px;
}

.target:hover {
  background-color: white;
  cursor: crosshair;
}

.indivCard:hover .target{
  display: block
}

.target:nth-of-type(2){
  right: 20px;
}

.target:nth-of-type(3){
  right: 40px;
}
</style>