<template>
  <div class="editor">
      <moveable-block :key="block.id" v-for="block in blocks">{{block}}</moveable-block>
  </div>
</template>

<script>
export default {
  props: ['blockarray'],
  name: 'blockEditor',
  data () {
    return {
      blocks: this.blockarray
    }
  }
}
</script>

<style>
.editor {
    height: 90vh;
    width: 100%;
}
</style>
