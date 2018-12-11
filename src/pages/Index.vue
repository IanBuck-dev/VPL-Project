<template>
  <q-page
    class="row justify-start items-center">
    <startBlock ref="startblock"></startBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color1"
      @mousemove.native="moveActive($event, 1)"
      @mouseup.native="moveEnd($event,1)"
      @mousedown.native="moveStart($event, 1)"
      :style="{'left': x1 + 'px', 'top': y1 + 'px'}"
      ref="bloc1"
      ></movableBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color2"
      :style="{'left': x2 + 'px', 'top': y2 + 'px'}"
      @mousedown.native="moveStart($event, 2)" @mouseup.native="moveEnd($event, 2)" @mousemove.native="moveActive($event, 2)" ref="bloc2"></movableBlock>
  </q-page>
</template>
//moveActive($event, 1)
//moveStartOnContainer($event)
<style>
</style>

<script>
import movableBlock from '../components/moveableBlock.vue'
import startBlock from '../components/startBlock.vue'

export default {
  name: 'PageIndex',
  components: {
    movableBlock,
    startBlock
  },
  data () {
    return {
      x1: 100,
      y1: 50,
      x2: 600,
      y2: 50,
      color1: 'blue',
      color2: 'indigo',
      origcolor1: 'blue',
      origcolor2: 'indigo',
      initX: 0,
      initY: 0,
      currentBlock: null,
      canbemoved: false
    }
  },
  methods: {
    moveStartOnContainer: function (event) {
      this.initX = event.offsetX
      this.initY = event.offsetY
      this.moving = true
      this.currentBlock = event.$el
      this.trackElement(event)
    },
    trackElement: function (event) {
      if (this.moving) {
        console.log(event)
      }
    },
    moveStart: function (event, index) {
      this.moving = true
      this.initX = event.pageX
      this.initY = event.pageY
      console.log(event)
      this['offsetInitX' + index] = event.offsetX
      this['offsetInitY' + index] = event.offsetY
    },
    moveActive: function (event, index) {
      if (this.moving) {
        this['x' + index] += event.offsetX - this['offsetInitX' + index]
        this['y' + index] += event.offsetY - this['offsetInitY' + index]

        var boundBox1 = this.$refs.bloc1.$el.getBoundingClientRect()
        var boundBox2 = this.$refs.bloc2.$el.getBoundingClientRect()

        var incompatable = !(boundBox1.right < boundBox2.left ||
                        boundBox1.left > boundBox2.right ||
                        boundBox1.bottom < boundBox2.top ||
                        boundBox1.top > boundBox2.bottom)

        var startBlockBox = this.$refs.startblock.$el.getBoundingClientRect()
        var compatable = !((boundBox1.right < startBlockBox.left || startBlockBox.right < boundBox1.left) || (boundBox1.bottom < startBlockBox.top || boundBox1.top > startBlockBox.bottom))

        if (incompatable) {
          this['x' + index] = this.initX
          this['y' + index] = this.initY
          this.moving = false
          this.color1 = 'red'
        }

        if (compatable) {
          this['x' + index] = startBlockBox.right
          this['y' + index] = startBlockBox.top - 100
        }
      }
    },
    moveEnd: function (event, index) {
      this.initX = event.pageX
      this.initY = event.page
      this.moving = false
    }
  }
}
</script>
