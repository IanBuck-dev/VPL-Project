<template>
  <div id="q-app">
    <div class="previewindowborder">
      <img src="../../assets/mark-rasmuson-108148-unsplash.jpg" v-bind:style="{width: setWidth? $(setWidth)+'px' : '200px'}">
    </div>
    <q-slider
      v-model="setWidth"
      @input="val => { setWidth = val }"
      :min="0" :max="10" :step="2" label :label-value="`${setWidth}px`" snap
    />
  </div>
</template>

<script>
export default {
  name: 'PreviewWindow'
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
</style>
