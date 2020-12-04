<template>
  <div class="indivCards">
      <div class="cards" v-for="(card, index) in cards" :key="index">
          <span v-for="(suit, index) in suits" :key="index" class="indivCard" @click="setCard(card, suit)">
              {{ card + "" + suit}}
          </span>

      </div>
    

  </div>
</template>

<script>
export default {
    props:[
        "setSelected"
    ],
    data(){
        return {
            cards: "A23456789TJQK".split(""),
            suits: "chds".split("")
        }
    },
    methods:{
        setCard(card, suit){
            this.setSelected({card,suit})

            let str = `${card}${suit}`
            alert(str)
        }
    }
}
</script>

<style scoped>
.indivCard{
    position: relative;
    display: inline-block;
    width: 25px;
    height: 25px;
    padding: 3px;
}
</style>