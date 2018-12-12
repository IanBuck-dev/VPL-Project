<template>
  <q-page
    @mouseup.native="moveEnd($event)"
    class="row justify-between items-center">
    <startBlock ref="startblock"></startBlock>
    <endBlock ref="endblock"></endBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color1"
      @mousemove.native="moveActive($event, 1)"
      @mouseup.native="moveEnd($event)"
      @mousedown.native="moveStart($event, 1)"
      :style="{'left': x1 + 'px', 'top': y1 + 'px'}"
      ref="bloc1"
      ></movableBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color2"
      :style="{'left': x2 + 'px', 'top': y2 + 'px'}"
      @mousedown.native="moveStart($event, 2)" @mousemove.native="moveActive($event, 2)" ref="bloc2"></movableBlock>
  </q-page>
</template>

<style>
</style>

<script>
import movableBlock from '../components/moveableBlock.vue'
import startBlock from '../components/startBlock.vue'
import endBlock from '../components/endBlock.vue'

export default {
  name: 'PageIndex',
  components: {
    movableBlock,
    startBlock,
    endBlock
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
    moveStart: function (event, index) {
      this.moving = true
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

        // if incompatible, then you get reset to where you first clicked
        if (incompatable) {
          this['x' + index] = this['offsetInitX' + index]
          this['y' + index] = this['offsetInitY' + index]
          this.moving = false
          this.color1 = 'red'
        }

        // lets 2 blocks stick together, if they are compatable
        // will be made available for more kinds of blocks
        if (compatable) {
          this['x' + index] = startBlockBox.right
          this['y' + index] = startBlockBox.top - 50
        }
      }
    },
    moveEnd: function (event) {
      this.moving = false
    }
  }
}
</script>
