<template>
  <q-page>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color1" class="q-ma-md movable"
      :style="{'left': x1 + 'px', 'top': y1 + 'px'}"
      @mousedown.native="moveStart($event, 1)" @mouseup.native="moveEnd($event,1)" @mousemove.native="moveActive($event, 1)" ref="bloc1"></movableBlock>
    <movableBlock :ht="'100px'" :wd="'100px'" :color="color2" class="q-ma-md movable"
      :style="{'left': x2 + 'px', 'top': y2 + 'px'}"
      @mousedown.native="moveStart($event, 2)" @mouseup.native="moveEnd($event, 2)" @mousemove.native="moveActive($event, 2)" ref="bloc2"></movableBlock>
  </q-page>
</template>

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
      origcolor2: 'yellow'
    }
  },
  methods: {
    toggleItem: function () {
      this.show = !this.show
    },
    receiveData: function (e) {
      this.blankData = e
    },
    moveStart: function (event, index) {
      this.moving = true
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
          this['color' + index] = 'green'
        } else {
          this['color' + index] = this['origcolor' + index]
          // this.color and this['color'] are equivalent
        }
      }
    }
  }
}
</script>
