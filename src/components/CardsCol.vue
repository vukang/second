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
  props: ["setSelected"],
  data() {
    return {
      cards: "A23456789TJQK".split(""),
      suits: "chds".split(""),
    };
  },
  methods: {
    doStuffWhenClicked() {},

    setCard(card, suit) {
      // toggle disabled class on card item (make it dark)

      // toggle object to write in
      // if active then set class
      //   if (suit == s) {
      //     console.log("hi bitches");
      //   }
      this.setSelected({ card, suit });

      let str = `${card}${suit}`;
      alert(str);
    },
  },
};
</script>

<style scoped>
.active {
  background-color: black;
}

.indivCard {
  position: relative;
  display: inline-block;
  width: 25px;
  height: 25px;
  padding: 3px;
  border-right: 1px solid black;
  border-left: 1px solid black;
}

.cards {
  /* border: 1px dashed black; */
}

.indivCard:hover {
  border: 1px solid black;
  cursor: pointer;
}
.indivCards {
  background-color: aliceblue;
}
</style>