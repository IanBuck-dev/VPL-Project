<template>
  <div class="movable"
    v-bind:class="{ deletedBlock: isDeleteBlock, endBlock: isEndBlock, startBlock: isStartBlock}"
  >
  <p v-if="normalBlock">{{block.name}}</p>
  <q-icon v-if="!normalBlock" name="delete_outline" size="95px" />
  </div>
</template>

<script>
export default {
  props: [
    'block'
  ],
  data () {
    return {
      normalBlock: true,
      isDeleteBlock: false,
      isEndBlock: false,
      isStartBlock: false
    }
  },
  created: function () {
    if (this.block.type === 10) {
      this.isDeleteBlock = true
      this.normalBlock = false
    }
    if (this.block.type === 9) {
      this.isEndBlock = true
    }
    if (this.block.type === 1) {
      this.isStartBlock = true
    }
  }
}
</script>

<style>
.movable {
  font-size: 25px;
  background-color: rgb(36, 34, 34);
  color: lightgray;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 0px;
  position: absolute;
  border: 2px solid rgb(46, 45, 45);
  border-radius: 5px;
  height: 100px;
  width: 100px;
  font-size: 1em;
  user-select: none;
  overflow: hidden;
}

.deletedBlock {
  background-color: rgb(36, 34, 34);
  color: white;
  border: none;
  font-size: 2em;
}

.startBlock {
  background-color: green;
  color: white;
  font-size: 2em;
}

.endBlock {
  background-color: rgb(36, 34, 34);
  color: white;
  border: none;
  font-size: 2em;
}
</style>
