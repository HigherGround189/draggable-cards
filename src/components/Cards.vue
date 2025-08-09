<template>
  <div class="card">
    <div class="card-inner">
      <div class="card-number">
        <span :class="underline ? 'underline' : ''">{{ num }}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: ["num"],
    data() {
      return {
        underline: false
      }
    },  
    mounted() {
      if (this.$props.num === 6 || this.$props.num === 9) {
        this.underline = true
      }
    }
  }
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

  .card {
    background: white;
    padding: 5px;
    /* opacity: 0.75; */

    width: 116px;
    height: 178px;
    border-radius: 5px;
    box-shadow:0 0 10px #aaaaaa;

    cursor: pointer;
  }

  .card:hover {
    opacity: 1;
  }

  .card-inner {
    background: hsl(153, 48%, 49%);
    border-radius: 5px;
    height: 100%;
    width: 100%;
  }

  .card-number {
    color: white;

    font-family: "Poppins", sans-serif;
    font-weight: bolder;
    font-size: 3.5rem;

    width: 100%;
    height: 100%;

    display: flex;
    justify-content: center;
    align-items: center;
  }

  .underline {
    text-decoration: underline;
    text-underline-offset: 0.5rem;
    text-decoration-thickness: 0.4rem;
  }

</style>