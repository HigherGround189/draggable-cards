<template>
  <div class="card" ref="card" :style="{ zIndex: zIndex }" @mousedown="zIndexIncrement">
    <div class="card-inner" :style="{ background: `var(--${colour})` }">
      <div class="card-number">
        <span :class="underline">{{ num }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import { createDraggable } from 'animejs'

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
      createDraggable(this.$refs.card, {
        container: 'body',
        containerFriction: 0.1,
        onGrab: () => this.$refs.card.style.zIndex = 9999999999999,
        onRelease: () => this.$refs.card.style.zIndex = this.zIndex
      })
    },
    zIndexIncrement() {
      const zIndexListMax = Math.max(...this.$props.zIndexList)
      this.$emit('update:zIndex', zIndexListMax + 1)
    }
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

  width: 116px;
  height: 178px;
  border-radius: 5px;
  box-shadow: 0 0 10px #aaaaaa;

  cursor: grab;
  user-select: none;
  touch-action: none;
  transition: box-shadow 0.15s ease-out;
}

.card:hover {
  box-shadow: 0 0 50px #aaaaaa;
}

.card:active {
  cursor: grabbing;
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
