<template>
  <div>
    <div :style="{'height': ht, 'width': wd, 'background': color}"></div>
  </div>
</template>

<script>
export default {
  props: ['ht', 'wd', 'color'],
  data () {
    return {
      dat: 'childData'
    }
  }
}
</script>

<style>
</style>
