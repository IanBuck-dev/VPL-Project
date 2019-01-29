<template>
  <div class="movable shadow-6"
    v-bind:class="{ deletedBlock: isDeleteBlock, endBlock: isEndBlock, startBlock: isStartBlock}"
  >
  <div v-if="isStartBlock" class="start">
    <span class="spacer"></span><p class="startText">{{block.name}}</p><div v-bind:class="{'connected': block.connected, 'disconnected': !block.connected}" class="startLine"></div>
  </div>
  <div v-if="isEndBlock" class="start">
    <div v-bind:class="{'connected': block.connected, 'disconnected': !block.connected}" class="endLine"></div><div class="spacer"></div><div class="startText">{{block.name}}</div>
  </div>
  <div v-if="normalBlock">
    <div class="block-items">
      <div>{{block.type}}</div>
      <div>{{block.name}}</div>
    </div>
    <div v-bind:class="{'connected': block.connected, 'disconnected': !block.connected}" class="line"></div>
  </div>
  <q-icon v-if="isDeleteBlock" name="delete_outline" size="95px" />
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
      isStartBlock: false,
      isConnected: false
    }
  },
  created: function () {
    if (this.block.type === 10) {
      this.isDeleteBlock = true
      this.normalBlock = false
    }
    if (this.block.type === 9) {
      this.isEndBlock = true
      this.normalBlock = false
    }
    if (this.block.type === 1) {
      this.isStartBlock = true
      this.normalBlock = false
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
  flex-direction: row;
  justify-content: center;
  padding: 0px;
  position: absolute;
  border-radius: 5px;
  height: 100px;
  width: 100px;
  font-size: 1em;
  user-select: none;
  overflow: hidden;
}

.block-items {
  height: 40px;
  width: 100px;
  color: white;
  overflow: hidden;
  word-break: break-all;
}

.deletedBlock {
  background-color: rgb(36, 34, 34);
  color: white;
  border: none;
  font-size: 2em;
}

.startBlock {
  background-color: green;
}

.endBlock {
  background-color: rgb(36, 34, 34);
  color: white;
}

.line {
  height: 20px;
  width: 100px;
  color: black;
  align-self: flex-end;
}

.start {
  height: 20px;
  width: 100px;
  display: flex;
  align-self: center;
}

.startText {
  height: 20px;
  width: 45px;
  font-size: 1em;
}

.startLine {
  height: 20px;
  width: 50px;
  border-top-left-radius: 8px;
  border-bottom-left-radius: 8px;
}

.endLine {
  height: 20px;
  width: 50px;
  border-top-right-radius: 8px;
  border-bottom-right-radius: 8px;
}

.connected {
  transition: background-color 1s;
  background-color: rgb(252, 176, 34);
}

.disconnected {
  background-color: rgb(248, 226, 184);
}

.spacer {
  height: 20px;
  width: 5px;
}
</style>
