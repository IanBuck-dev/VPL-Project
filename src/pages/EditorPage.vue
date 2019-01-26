<template>
  <q-page v-on:block-created="createBlock(name, type)" :key="componentKey">
     <block
      :key="block.id"
      v-for="block in blocks"
      :block="block"
      :style="{'left': block.x + 'px', 'top': block.y + 'px'}"
      @mousemove.native="moveActive($event, block.id)"
      @mouseup.native="moveEnd()"
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
          type: 9,
          x: 500,
          y: 200
        },
        {
          id: 3,
          name: 'Type 2',
          type: 2,
          x: 200,
          y: 100
        },
        {
          id: 4,
          name: 'Type 3',
          type: 3,
          x: 400,
          y: 100
        },
        {
          id: 5,
          name: 'Delete',
          type: 10,
          x: 650,
          y: 500
        }
      ],
      removeBlockTimeout: false,
      counterForId: 6,
      componentKey: 0
    }
  },
  created () {
    this.$root.$on('block-created', this.createBlock)
    this.$root.$on('new-project', this.forceReload)
  },
  methods: {
    // detects the collision of two blocks
    // if two blocks collide, it checks if they can go together
    // type 1 and 2, and type 2 and 3 go together; type 1 and 3 don't go together
    // if the blocks are compatable, they clip together, if not the moving block gets repelled
    detectCollisions: function (block, id) {
      var movingblock = this.blocks.find(function (element) {
        return element.id === id
      })

      var touching = (
        (block.x + 50 > movingblock.x - 50 && movingblock.y + 50 > block.y - 50) && (block.x - 50 < movingblock.x + 50 && movingblock.y - 50 < block.y + 50) && !(block.id === movingblock.id)
      )

      var compatable = (
        (((block.type === 1) && (movingblock.type === 2)) || ((block.type === 2) && (movingblock.type === 3))) ||
        (((movingblock.type === 1) && (block.type === 2)) || ((movingblock.type === 2) && (block.type === 3)))
      )

      var incompatable = (
        ((block.type === 1) && (movingblock.type === 3)) || ((movingblock.type === 1) && (block.type === 3))
      )

      var deleteBlock = (
        block.type === 10
      )

      if (touching && compatable) {
        movingblock.x = block.x + 100
        movingblock.y = block.y
        this.moving = false
      }

      if (touching && incompatable) {
        movingblock.x = block.x
        movingblock.y = block.y - 150
        this.moving = false
      }
      if (touching && deleteBlock) {
        this.deleteBlock(movingblock.id)
      }
    },
    isTouching: function (block, id) {
      var movingblock = this.blocks.find(function (element) {
        return element.id === id
      })
      var touching = (
        (block.x + 50 > movingblock.x - 50 && movingblock.y + 50 > block.y - 50) && (block.x - 50 < movingblock.x + 50 && movingblock.y - 50 < block.y + 50) && !(block.id === movingblock.id)
      )

      if (touching) {
        this.removeBlockTimeout = true
        setTimeout(function () {
          this.removeBlockTimeout = false
        }, 1500)
      }
    },
    moveStart: function (event, index) {
      this.moving = true

      this.blocks.forEach(element => {
        this.isTouching(element, index)
      })
    },
    moveActive: function (event, id) {
      if (this.moving && !this.removeBlockTimeout) {
        console.log(event)
        this.blocks.find(function (element) {
          return element.id === id
        }).x = event.x - 50
        this.blocks.find(function (element) {
          return element.id === id
        }).y = event.y - 100
        this.blocks.forEach(element => {
          this.detectCollisions(element, id)
        })
      }
    },
    moveEnd: function () {
      this.moving = false
    },
    createBlock: function (name, type) {
      var newBlock = {
        id: this.counterForId,
        name: name,
        type: type,
        x: 200,
        y: 50
      }
      this.counterForId += 1
      this.blocks.push(newBlock)
      console.log(newBlock)
    },
    deleteBlock: function (id) {
      var blockToDelete = this.blocks.findIndex(x => x.id === id)

      console.log(blockToDelete)
      this.blocks.splice(blockToDelete, 1)
      console.log('Block deleted!')
    },
    forceReload: function () {
      this.componentKey += 1
      console.log(this.componentKey)
    }
  }
}
</script>

<style>
</style>
