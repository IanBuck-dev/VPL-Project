<template>
  <q-page
    @mousemove.native="moveActive($event, 1)"
    @mouseup.native="moveEnd($event,1)"
    @mousedown.native="moveStart($event, 1)"
    >
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color1" class="q-ma-md movable" id="block1"
      :style="{'left': x1 + 'px', 'top': y1 + 'px'}"
      @mousedown.native="moveStart($event, 1)" ref="bloc1"></movableBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color2" class="q-ma-md movable"
      :style="{'left': x2 + 'px', 'top': y2 + 'px'}"
      @mousedown.native="moveStart($event, 2)" @mouseup.native="moveEnd($event, 2)" @mousemove.native="moveActive($event, 2)" ref="bloc2"></movableBlock>
  </q-page>
</template>
//moveActive($event, 1)
//moveStartOnContainer($event)
<style>
.movable {
  display: inline-block;
  padding: 0px;
  position: absolute;
}
</style>

<script>
import navbar from '../components/Navbar.vue'
import movableBlock from '../components/moveableBlock.vue'

export default {
  name: 'PageIndex',
  components: {
    navbar,
    movableBlock
  },
  data () {
    return {
      x1: 200,
      y1: 200,
      x2: 400,
      y2: 400,
      color1: 'blue',
      color2: 'yellow',
      origcolor1: 'blue',
      origcolor2: 'yellow',
      initX: 0,
      initY: 0,
      currentBlock: null
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

        var overlap = !(boundBox1.right < boundBox2.left ||
                        boundBox1.left > boundBox2.right ||
                        boundBox1.bottom < boundBox2.top ||
                        boundBox1.top > boundBox2.bottom)

        if (overlap) {
          this['x' + index] = this.initX
          this['y' + index] = this.initY
          this.moving = false
          this.color1 = 'red'
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
