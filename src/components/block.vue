<template>
  <div class="movable">{{block.name}}</div>
</template>

<script>
export default {
  props: ['block']
}
</script>

<style>
.movable {
  font-size: 25px;
  color: #fff;
  display: inline-block;
  padding: 0px;
  position: absolute;
  border: 2px solid rgb(46, 45, 45);
  border-radius: 5px;
}
</style>
