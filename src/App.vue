<template>
  <div class="card-container">
    <Cards v-for="(colour, index) in cardColourList" :num="index" :colour="colour" v-model:zIndex="zIndexList[index]" :zIndexList="zIndexList"/>
  </div>
</template>

<script>
  import Cards from './components/Cards.vue';

  function getRandomIntInclusive(min, max) {
    const minCeiled = Math.ceil(min)
    const maxFloored = Math.floor(max)
    return Math.floor(Math.random() * (maxFloored - minCeiled + 1) + minCeiled)
  }
  
  const NUM_OF_CARDS = 10

  export default {
    components: { Cards },
    data() {
      return {
        cardColourList: [],
        zIndexList: []
      }
    },
    methods: {

    },
    created() {
      let randNum;
      const colourList = ["red", "yellow", "green", "blue"]
      for (let i=0; i <= NUM_OF_CARDS; i++) {
        randNum = getRandomIntInclusive(0, 3)
        this.cardColourList.push(colourList[randNum])
        this.zIndexList.push(0)
      }
    }
  }
</script>

<style scoped>
  .card-container {
    display: flex;
    gap: 5vw; 
    flex-wrap: wrap;
  }
</style>