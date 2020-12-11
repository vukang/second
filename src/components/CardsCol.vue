<template>
  <div class="indivCards">
    <div class="cards" v-for="(card, index) in kartenstapel" :key="index">
      <span
        :class="{
          indivCard: true,
          spades: card.suit.includes('♠️'),
          clubs: card.suit.includes('♣️'),
          hearts: card.suit.includes('♥️'),
          diamonds: card.suit.includes('♦️'),
          hero: heroC.includes(card),
          board: boardC.includes(card),
          vill: villC.includes(card),
        }"
        @click="
          (e) => {
            copyFreiSlot(card);
          }
        "
      >
        {{ card.value }}

        <div
          class="target"
          @click="
            (e) => {
              kopiereKarte(card, 'heroC', 2);
            }
          "
        >
          H
        </div>

        <div
          class="target"
          @click="
            (e) => {
              kopiereKarte(card, 'boardC', 5);
            }
          "
        >
          C
        </div>

        <div
          class="target"
          @click="
            (e) => {
              kopiereKarte(card, 'villC', 2);
            }
          "
        >
          V
        </div>
      </span>
    </div>
    <button @click="reloadPage()">Reset all</button>
  </div>
</template>

<script>
export default {
  props: [
    "heroC",
    "villC",
    "boardC",
    "setH",
    "setC",
    "setV",
    "resetAll",
    "kopiereKarte",
    "kartenstapel",
  ],
  data() {
    return {
      cards: "A23456789TJQK".split(""),
      suits: ["♣️", "♦️", "♥️", "♠️"],
    };
  },
  methods: {
    reloadPage() {
      this.resetAll();
    },

    settingH(karte) {
      this.setH(karte);
    },

    settingC(karte) {
      this.setC(karte);
    },

    settingV(karte) {
      this.setV(karte);
    },

    copyFreiSlot(card) {
      console.log("in copyFreiSlot...");
      console.log(card.value);

      if (this.heroC.length == 2 && this.villC.length == 2) {
        // push to boardC
        this.kopiereKarte(card, "boardC", 5);
        console.log(this.boardC.length, "Board#");
      }

      if (this.heroC.length < 2) {
        this.kopiereKarte(card, "heroC", 2);
        console.log(this.heroC.length, "Hero#");
      }

      if (this.villC.length < 2) {
        this.kopiereKarte(card, "villC", 2);
        console.log(this.villC.length, "Vill#");
      }

      console.log("...end");
    },
  },
};
</script>

<style scoped>
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

.cards {
  display: inline;
}

.indivCard.hero {
  background-color: darkkhaki !important;
}
.indivCard.board {
  background-color: yellow !important;
}
.indivCard.vill {
  background-color: azure !important;
}

.indivCard.spades {
  background-color: rgba(34, 32, 32, 0.459);
  color: black;
}
.indivCard.clubs {
  background-color: rgba(97, 201, 97, 0.582);
  color: black;
}
.indivCard.hearts {
  background-color: rgba(245, 73, 73, 0.644);
  color: black;
}
.indivCard.diamonds {
  background-color: rgba(75, 75, 252, 0.559);
  color: black;
}

.indivCard:hover {
  border: 1px solid black;
  background-color: rgba(128, 128, 128, 0.23);
}
.indivCards {
  display: border-box;
}

/* target = small span below inside card */

.target {
  display: none;
  position: absolute;
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

.indivCard:hover .target {
  display: block;
}

.target:nth-of-type(2) {
  right: 20px;
}

.target:nth-of-type(3) {
  right: 40px;
}
</style>