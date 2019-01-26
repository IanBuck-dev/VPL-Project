<template>
  <div class="movable"
    v-bind:class="{ deletedBlock: isDeleteBlock, endBlock: isEndBlock, startBlock: isStartBlock}"
  >
    {{block.id}} <br>
    {{block.name}}
  </div>
</template>

<script>
export default {
  props: [
    'block'
  ],
  data () {
    return {
      isDeleteBlock: false,
      isEndBlock: false,
      isStartBlock: false
    }
  },
  created: function () {
    if (this.block.type === 10) {
      this.isDeleteBlock = true
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
  background-color: grey;
  display: inline-block;
  padding: 0px;
  position: absolute;
  border: 2px solid rgb(46, 45, 45);
  border-radius: 5px;
  height: 100px;
  width: 100px;
  font-size: 1.2em;
  user-select: none;
  overflow: scroll;
}

.deletedBlock {
  background-color: black;
  color: white;
}

.startBlock {
  background-color: green;
  color: white;
}
</style>
