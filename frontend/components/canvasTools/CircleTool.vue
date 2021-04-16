<template>
  <div></div>
</template>

<script>
import { v4 } from 'uuid'
import { mapState } from 'vuex'
import customEvents from '~/utils/customEvents'
import WhitebirdLogger from '~/utils/WhitebirdLogger'

const logger = new WhitebirdLogger('CircleTool.vue')

export default {
  props: {
    canvas: {
      type: Object,
      required: true,
    },
  },
  computed: {
    ...mapState({
      canvasID: (state) => state.canvas.id,
      testObject: (state) => state.canvas.testObject,
    }),
  },
  mounted() {
    this.$nuxt.$on(customEvents.canvasTools.circle, (payload) => {
      this.canvas.isDrawingMode = false
      this.createCircle(payload)
    })
  },
  methods: {
    createCircle(options) {
      // Restore to the default zoom level.
      this.canvas.setZoom(1)
      
      // Calculate the initial position according to the view port.
      var topLeftPos = this.canvas.calcViewportBoundaries().tl
      var offset = 100

      var initLeft = topLeftPos.x + offset
      var initTop = topLeftPos.y + offset

      const circle = new fabric.Circle({
        left: initLeft,
        top: initTop,
        radius: 25,
        stroke: options.stroke,
        fill: options.fill,
        whitebirdData: { id: v4() },
      })

      this.canvas.add(circle).setActiveObject(circle)
      logger.log(circle)
      this.canvas.renderAll()
    },
  },
}
</script>
