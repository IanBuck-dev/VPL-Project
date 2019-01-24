<template>
  <div id="q-app">
    <div class="previewindowborder">
      <img src="../../assets/mark-rasmuson-108148-unsplash.jpg" v-bind:style="{width: setWidth? setWidth+'px' : '200px'}">
    </div>
    <q-slider id="zoomBar"
      :model="setWidth"
      color="amber"
      @input="val => { setWidth = val }"
      :min="200" :max="1200" :step="100" label :label-value="(setWidth-200)/10+'%'" snap
    />
  </div>
</template>

<script>
export default {
  name: 'PreviewWindow',
  data () {
    return {
      setWidth: 200
    }
  }
}
</script>

<style>
.previewindowborder {
  margin: 10px;
  border: 2px solid black;
  height: 10em;
  width: 94%;
  display: grid;
  align-items: center;
  justify-items: center;
  overflow: hidden;
}

#zoomBar {
  padding: 0 30px;
}
</style>
