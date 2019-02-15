<template>
  <q-page class="background-editor" v-on:block-created="createBlock(name, type)">
     <block
      :key="block.id"
      v-for="block in blocks"
      :block="block"
      :style="{'left': block.x + 'px', 'top': block.y + 'px'}"
      @mousemove.native="moveActive($event, block)"
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
          name: 'Start',
          type: 1,
          x: 50,
          y: 200,
          connected: false,
          canBeConnected: false
        },
        {
          id: 2,
          name: 'End',
          type: 9,
          x: 1000,
          y: 200,
          connected: false,
          canBeConnected: false
        },
        {
          id: 3,
          name: 'Type 2',
          type: 2,
          x: 200,
          y: 100,
          connected: false,
          canBeConnected: false
        },
        {
          id: 4,
          name: 'Type 3',
          type: 3,
          x: 400,
          y: 100,
          connected: false,
          canBeConnected: false
        },
        {
          id: 5,
          name: 'Delete',
          type: 10,
          x: 1000,
          y: 500,
          connected: false,
          canBeConnected: false
        },
        {
          id: 6,
          name: 'Procedure',
          type: 3,
          x: 700,
          y: 500,
          connected: false,
          canBeConnected: false
        }
      ],
      removeBlockTimeout: false,
      counterForId: 7,
      newBlockTouching: false,
      notify: {
        label: 'Confirm',
        icon: 'done_all',
        handler: (index) => {
          this.$q.dialog({
            title: 'Confirm delete',
            message: 'Are you sure you want to delete this block?',
            ok: 'Agree',
            cancel: 'Disagree'
          }).then(() => {
            this.$q.notify({
              message: 'Agreed!',
              position: 'bottom-left'
            })
            this.blocks.splice(index, 1)
          }).catch(() => {
            this.$q.notify({
              message: 'Disagreed!',
              position: 'bottom-left'
            })
            this.blocks[index].y = this.blocks[index].y - 100
          })
        }
      },
      notifyCantDelete: {
        label: 'Delete unsuccesfull',
        icon: 'done_all',
        handler: (index) => {
          this.$q.dialog({
            title: 'Can\'t delete',
            message: 'You can\'t delete this block!',
            ok: 'Agree'
          }).then(() => {
            this.blocks[index].y = this.blocks[index].y - 100
          })
        }
      },
      notifyUpload: {
        label: 'Upload Data',
        icon: 'cloud_upload',
        handler: () => {
          this.$q.dialog(
            {
              title: 'Upload data',
              message: 'Here you can upload data like pictures. The first one will be visible in the preview window!',
              ok: 'Agree',
              cancel: 'Cancel'
            }
          ).then(() => {})
        }
      }
    }
  },
  created () {
    this.$root.$on('block-created', this.createBlock)
    this.$root.$on('new-project', this.forceReload)
    this.notifyUpload.handler()
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
        (((block.type === 1) && (movingblock.type === 2)) || ((block.type === 2) && (movingblock.type === 1))) ||
        (((movingblock.type === 3) && (block.type === 2)) || ((movingblock.type === 2) && (block.type === 3))) ||
        (((movingblock.type === 2) && (block.type === 2)) || ((movingblock.type === 2) && (block.type === 2))) ||
        (((movingblock.type === 3) && (block.type === 3)) || ((movingblock.type === 3) && (block.type === 3)))
      )

      var endBlock = (
        (((movingblock.type === 3) && (block.type === 9)) || ((movingblock.type === 9) && (block.type === 3)))
      )

      var incompatable = (
        (((block.type === 1) && (movingblock.type === 3)) || ((movingblock.type === 1) && (block.type === 3))) ||
        (((block.type === 2) && (movingblock.type === 9)) || ((movingblock.type === 2) && (block.type === 9))) ||
        (((block.type === 1) && (movingblock.type === 9)) || ((movingblock.type === 1) && (block.type === 9)))
      )

      var deleteBlock = (
        block.type === 10
      )

      if (compatable) {
        block.canBeConnected = true
      }

      if (endBlock) {
        block.canBeConnected = true
      }

      if (touching && compatable) {
        if (movingblock.x > block.x) {
          movingblock.x = block.x + 100
        } else {
          movingblock.x = block.x - 100
        }
        movingblock.y = block.y
        this.moving = false
        movingblock.connected = true
        block.connected = true
      }

      if (touching && endBlock) {
        console.log(movingblock.type)
        if (movingblock.type === 9) {
          movingblock.x = block.x + 100
        } else {
          movingblock.x = block.x - 100
        }
        movingblock.y = block.y
        this.moving = false
        movingblock.connected = true
        block.connected = true
        this.$root.$emit('ready-to-execute')
      }

      if (touching && incompatable) {
        movingblock.x = block.x
        movingblock.y = block.y - 150
        this.moving = false
        this.$q.notify({
          message: 'These two blocks don\'t work together!',
          position: 'bottom-left',
          color: 'negative'
        })
      }
      if (touching && deleteBlock) {
        this.deleteBlock(movingblock)
      }
    },
    isTouching: function (block, id) {
      var movingblock = this.blocks.find(function (element) {
        return element.id === id
      })
      var touching = (
        (((block.x + 50 > movingblock.x - 50 && movingblock.y + 50 > block.y - 50) && (block.x - 50 < movingblock.x + 50 && movingblock.y - 50 < block.y + 50)) ||
        ((block.x - 50 > movingblock.x + 50 && movingblock.y - 50 > block.y + 50) && (block.x + 50 < movingblock.x - 50 && movingblock.y + 50 < block.y - 50))) &&
        !(block.id === movingblock.id)
      )

      if (touching) {
        this.removeBlockTimeout = true
        this.newBlockTouching = true
        setTimeout(function () {
          this.removeBlockTimeout = false
        }, 2500)
      }
    },
    moveStart: function (event, index) {
      this.moving = true

      this.blocks.forEach(element => {
        this.isTouching(element, index)
      })
    },
    moveActive: function (event, block) {
      var moving = (this.moving && !this.removeBlockTimeout) && !(block.type === 10)
      if (moving) {
        block.connected = false
        block.x = event.x - 50
        block.y = event.y - 100
        this.blocks.forEach(element => {
          this.detectCollisions(element, block.id)
        })
      }
    },
    moveEnd: function () {
      this.moving = false
      this.blocks.forEach(element => {
        element.canBeConnected = false
      })
    },
    createBlock: function (name, type) {
      var newBlock = {
        id: this.counterForId,
        name: name,
        type: type,
        x: 200,
        y: 400,
        connected: false
      }
      this.counterForId += 1
      var newIndex = this.blocks.length
      this.$set(this.blocks, newIndex, newBlock)

      console.log(newBlock)
    },
    deleteBlock: function (block) {
      var deletable = !((block.type === 1) || (block.type === 9))
      var index = this.blocks.findIndex(x => x.id === block.id)
      if (deletable) {
        this.notify.handler(index)
      } else {
        this.notifyCantDelete.handler(index)
      }
    },
    forceReload: function () {
      this.$q.forceReload()
    }
  }
}
</script>

<style>
.background-editor {
  background: linear-gradient(45deg, #45484d 0%,#000000 100%);
}
</style>
