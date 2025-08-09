<template>
  <div class="card" ref="card">
    <div class="card-inner" :style="{ background: `var(--${colour})` }">
      <div class="card-number">
        <span :class="underline ? 'underline' : ''">{{ num }}</span>
      </div>
    </div>
  </div>
</template>

<script>
  import interact from 'interactjs';


  export default {
    props: ["num", "colour"],
    data() {
      return {
        underline: false
      }
    },
    methods: {
      checkNum() {
        if (this.$props.num === 6 || this.$props.num === 9) {
          this.underline = true
        }
      },

      makeDraggable() {
        // const cardPositionRaw = this.$refs.card.getBoundingClientRect()
        const position = { x: 0, y: 0 };

        console.log(position)

        interact(this.$refs.card).draggable({
          listeners: {
            start (event) {
              console.log(event.type, event.target)
            },
            move (event) {
              position.x += event.dx
              position.y += event.dy

              event.target.style.transform =
                `translate(${position.x}px, ${position.y}px)`
            },
          }
        })
      }
    },
    mounted() {
      this.checkNum()
      this.makeDraggable()
    }
  }

</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

  .card {
    background: white;
    padding: 5px;
    /* opacity: 0.75; */

    width: 6.05vw;
    aspect-ratio: 116 / 178;
    border-radius: 5px;
    box-shadow:0 0 10px #aaaaaa;

    cursor: pointer;
    user-select: none;
    touch-action: none
  }

  .card:hover {
    opacity: 1;
  }

  .card-inner {
    --red: hsl(0, 80%, 40%);
    --green: hsl(150, 50%, 50%);
    --blue: hsl(235, 50%, 40%);
    --yellow: hsl(50, 75%, 50%);

    background: var(--blue);
    border-radius: 5px;
    height: 100%;
    width: 100%;
  }

  .card-number {
    color: white;

    font-family: "Poppins", sans-serif;
    font-weight: bolder;
    font-size: 3.5vw;

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