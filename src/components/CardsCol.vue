<template>
  <div class="indivCards">
    <div class="cards" v-for="(card, index) in cards" :key="index">
      <span
        v-for="(suit, index) in suits"
        :key="index"
        class="indivCard"
        @click="
          (e) => {
            e.target.classList.toggle('active');
            e.target.classList.toggle('indivCard');
            doStuffWhenClicked(e);
            setCard(card, suit);
          }
        "
      >
        {{ card + "" + suit }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: ["setSelected", "setHole"],
  data() {
    return {
      cards: "A23456789TJQK".split(""),
      suits: ["♣️", "♦️", "♥️", "♠️"],
      // suits: "cdhs".split(""),
    };
  },
  methods: {
    doStuffWhenClicked(e) {
      console.log(e);
      console.log(e.currentTarget.textContent);
      this.setHole(e.currentTarget.textContent);
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
  width: 25px;
  height: 25px;
  padding: 3px;
  border-right: 1px solid black;
  border-left: 1px solid black;
  cursor: cell;
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
</style>