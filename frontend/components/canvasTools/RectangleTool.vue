<template>
  <div></div>
</template>

<script>
import { v4 } from 'uuid'
import customEvents from '~/utils/customEvents'

export default {
  props: {
    canvas: {
      type: Object,
      required: true,
    },
  },
  mounted() {
    this.$nuxt.$on(customEvents.canvasTools.rectangle, (payload) => {
      this.canvas.isDrawingMode = false
      this.createRectangle(payload)
    })
  },
  methods: {
    createRectangle(options) {
      // Restore to the default zoom level.
      this.canvas.setZoom(1)
      
      // Calculate the initial position according to the view port.
      var topLeftPos = this.canvas.calcViewportBoundaries().tl
      var offset = 100

      var initLeft = topLeftPos.x + offset
      var initTop = topLeftPos.y + offset

      const rect = new fabric.Rect({
        left: initLeft,
        top: initTop,
        width: 50,
        height: 50,
        stroke: options.stroke,
        fill: options.fill,
        whitebirdData: { id: v4() },
      })

      this.canvas.add(rect).setActiveObject(rect)
      this.canvas.renderAll()
    },
  },
}
</script>
