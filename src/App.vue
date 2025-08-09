<template>
  <div class="card-container">
    <Cards v-for="n in 10" :num="n - 1" :colour="colour()"/>
  </div>
</template>

<script>
  import Cards from './components/Cards.vue';

  function getRandomIntInclusive(min, max) {
    const minCeiled = Math.ceil(min)
    const maxFloored = Math.floor(max)
    return Math.floor(Math.random() * (maxFloored - minCeiled + 1) + minCeiled)
  }

  export default {
    components: { Cards },
    data() {
      return {
        colourMap: ["red", "yellow", "green", "blue"]
      }
    },
    methods: {
      colour() {
        const randNum = getRandomIntInclusive(0, 3)
        return this.colourMap[randNum]
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