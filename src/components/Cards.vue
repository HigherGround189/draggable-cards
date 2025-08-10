<template>
  <div
    class="card"
    ref="card"
    :style="{ zIndex: zIndex }"
    v-on="{ click: zIndexIncrement, mousedown: mouseDown, mouseup: mouseUp }"
  >
    <div class="card-inner" :style="{ background: `var(--${colour})` }">
      <div class="card-number">
        <span :class="underline">{{ num }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import interact from 'interactjs'

export default {
  props: ['num', 'colour', 'zIndex', 'zIndexList'],
  data() {
    return {}
  },
  computed: {
    underline() {
      let underlineClass = ''
      if (this.$props.num === 6 || this.$props.num === 9) {
        underlineClass = 'underline'
      }

      return underlineClass
    },
  },
  methods: {
    makeDraggable() {
      const position = { x: 0, y: 0 }

      interact(this.$refs.card).draggable({
        modifiers: [
          interact.modifiers.restrictRect({
            restriction: 'body',
            endOnly: true,
          }),
        ],
        cursorChecker: () => null,
        listeners: {
          move(event) {
            position.x += event.dx
            position.y += event.dy

            event.target.style.transform = `translate(${position.x}px, ${position.y}px)`
          },
        },
      })
    },
    zIndexIncrement() {
      const zIndexListMax = Math.max(...this.$props.zIndexList)
      this.$emit('update:zIndex', zIndexListMax + 1)
    },
    mouseDown() {
      this.$refs.card.style.zIndex = 9999999999999
      document.style
    },
    mouseUp() {
      this.$refs.card.style.zIndex = this.zIndex
    },
  },
  mounted() {
    this.makeDraggable()
  },
}
</script>

<style scoped>
.card {
  background: white;
  padding: 5px;
  /* opacity: 0.75; */

  width: 116px;
  height: 178px;
  border-radius: 5px;
  box-shadow: 0 0 10px #aaaaaa;

  cursor: grab;
  user-select: none;
  touch-action: none;
  transition: 0.3s transform;
}

.card:hover {
  opacity: 1;
}

.card:active {
  cursor: grabbing;
  transition: none;
}

.card-inner {
  --red: hsl(0, 80%, 40%);
  --green: hsl(150, 50%, 50%);
  --blue: hsl(235, 50%, 40%);
  --yellow: hsl(50, 75%, 50%);

  background: var(--green);
  border-radius: 5px;
  height: 100%;
  width: 100%;
}

.card-number {
  color: white;

  font-family: 'Poppins', sans-serif;
  font-weight: bolder;
  font-size: 66px;

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
