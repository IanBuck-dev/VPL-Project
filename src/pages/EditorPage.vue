<template>
  <q-page>
     <block
      :key="block.id"
      v-for="block in blocks"
      :block="block"
      :style="{'left': block.x + 'px', 'top': block.y + 'px'}"
      @mousemove.native="moveActive($event, block.id)"
      @mouseup.native="moveEnd($event, block.id)"
      @mousedown.native="moveStart($event, block.id)"
      ></block>
  </q-page>
</template>

<script>
import block from '../components/block.vue'

export default {
  components: {
    block
  },
  data () {
    return {
      blocks: [
        {
          id: 1,
          name: 'Startblock',
          type: 1,
          x: 100,
          y: 200
        },
        {
          id: 2,
          name: 'Endblock',
          type: 1,
          x: 500,
          y: 200
        },
        {
          id: 3,
          name: 'Random',
          type: 1,
          x: 300,
          y: 200
        }
      ],
      removeBlockTimeout: false
    }
  },
  methods: {
    detectCollisions: function (block, index) {
      var movingblock = this.blocks[index - 1]

      var touching = (
        (block.x + 50 > movingblock.x - 50 && movingblock.y + 50 > block.y - 50) && (block.x - 50 < movingblock.x + 50 && movingblock.y - 50 < block.y + 50) && !(block.id === movingblock.id)
      )

      if (touching) {
        movingblock.x = block.x + 100
        movingblock.y = block.y
        this.moving = false
      }
      console.log(touching)
    },
    isTouching: function (block, index) {
      var movingblock = this.blocks[index - 1]
      var touching = (
        (block.x + 50 > movingblock.x - 50 && movingblock.y + 50 > block.y - 50) && (block.x - 50 < movingblock.x + 50 && movingblock.y - 50 < block.y + 50) && !(block.id === movingblock.id)
      )

      if (touching) {
        this.removeBlockTimeout = true
        setTimeout(function () {
          this.removeBlockTimeout = false
        }, 500)
      }
    },
    moveStart: function (event, index) {
      this.moving = true

      this.blocks.forEach(element => {
        this.isTouching(element, index)
      })
    },
    moveActive: function (event, index) {
      if (this.moving && !this.removeBlockTimeout) {
        console.log(event)
        this.blocks[index - 1].x = event.x - 50
        this.blocks[index - 1].y = event.y - 100
        this.blocks.forEach(element => {
          this.detectCollisions(element, index)
        })
      }
    },
    moveEnd: function (event, index) {
      this.moving = false
    }
  }
}
</script>

<style>
</style>
