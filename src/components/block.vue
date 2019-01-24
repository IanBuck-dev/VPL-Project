<template>
  <div class="movable">
    {{block.id}} <br>
    {{block.name}}
  </div>
</template>

<script>
export default {
  props: [
    'block'
  ]
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
</style>
