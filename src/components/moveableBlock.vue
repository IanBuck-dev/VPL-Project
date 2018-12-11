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
  },
  methods: {
    function () {
      this.$emit('emitted', this.dat)
    }
  }
}
</script>

<style>
</style>
