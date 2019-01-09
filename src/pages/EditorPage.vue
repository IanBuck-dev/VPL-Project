<template>
  <q-page>
     <block :key="block.id" v-for="block in blocks"></block>
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
      movableStartblock: {
        id: 1,
        name: 'Startblock',
        x: 100,
        y: 200
      },
      movableEndblock: {
        id: 2,
        name: 'Endblock',
        x: 600,
        y: 200
      },
      blocks: [
        this.movableStartblock,
        this.movableEndblock
      ]
    }
  }
}
</script>

<style>
</style>
