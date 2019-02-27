<template>
  <div>
    <div
      ref="container"
      class="container"
    ></div>
    <div class="point"></div>
    <div class="point"></div>
    <div class="point"></div>
  </div>
</template>

<script>

import { TweenLite } from 'gsap'
import Draggable from 'gsap/Draggable'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  mounted () {
    const { container } = this.$refs
    const gridWidth = 100
    const gridHeight = 100
    const gridRows = 6
    const gridColumns = 9

    TweenLite.set(container, { height: gridRows * gridHeight + 1, width: gridColumns * gridWidth + 1 })
    TweenLite.set('.point', { width: gridWidth, height: gridHeight, lineHeight: gridHeight + 'px' })

    Draggable.create('.point', {
      edgeResistance: 0.65,
      type: 'x,y',
      autoScroll: true,
      liveSnap: {
        x: (endValue) => Math.round(endValue / gridWidth) * gridWidth,
        y: (endValue) => Math.round(endValue / gridHeight) * gridHeight
      }
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.point {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: red;
}

.container {
  border: 1px solid red;
}
</style>
