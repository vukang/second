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
      //   suits: "♣️♦️♥️♠️".split(""),
      suits: "cdhs".split(""),
    };
  },
  methods: {
    doStuffWhenClicked(e) {
      console.log(e);
      console.log(e.currentTarget.textContent);
      this.setHole(e.currentTarget.textContent);
    },

    setCard(card, suit) {
      // toggle disabled class on card item (make it dark)

      // toggle object to write in
      // if active then set class
      //   if (suit == s) {
      //     console.log("hi bitches");
      //   }
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

.indivCard:hover {
  border: 1px solid black;
}
.indivCards {
  background-color: aliceblue;
}
</style>