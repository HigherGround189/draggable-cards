<template>
  <h1>Draggable Cards</h1>

  <div class="card-container">
    <Cards
      v-for="(colour, index) in cardColourList"
      :key="index"
      :num="index"
      :colour="colour"
      v-model:zIndex="zIndexList[index]"
      :zIndexList="zIndexList"
    />
  </div>
</template>

<script>
import Cards from './components/Cards.vue'

function getRandomIntInclusive(min, max) {
  const minCeiled = Math.ceil(min)
  const maxFloored = Math.floor(max)
  return Math.floor(Math.random() * (maxFloored - minCeiled + 1) + minCeiled)
}

const NUM_OF_CARDS = 9

export default {
  components: { Cards },
  data() {
    return {
      cardColourList: [],
      zIndexList: [],
    }
  },
  methods: {},
  created() {
    let randNum
    const colourList = ['red', 'yellow', 'green', 'blue']
    for (let i = 0; i <= NUM_OF_CARDS; i++) {
      randNum = getRandomIntInclusive(0, 3)
      this.cardColourList.push(colourList[randNum])
      this.zIndexList.push(0)
    }
  },
}
</script>

<style scoped>
h1 {
  color: white;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 5.5rem;
  text-align: center;
  margin-bottom: 10vh;
  text-shadow: 0 0 5px #aaaaaa;
  user-select: none;
}

.card-container {
  display: flex;
  gap: 5vw;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
