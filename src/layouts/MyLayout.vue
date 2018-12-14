<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-drawer
      row
      side="right"
      v-model="rightDrawerOpen"
      :content-class="$q.theme === 'mat' ? 'bg-grey-2' : null"
      class="layout-drawer"
    >
      <previewWindow></previewWindow>
      <q-collapsible indent label="Pre-Processing">
        <q-item v-close-overlay @click.native="createNewBlock">Edge Extraction</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Denoising</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Blur Reduction</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Sharpening</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Brightness</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Converting Color Spaces</q-item>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Line Segmentation">
        <q-item v-close-overlay @click.native="createNewBlock">Text Split</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Picture Split</q-item>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Optical Character Recognition">
        <q-item v-close-overlay @click.native="createNewBlock">Word and Character Processing</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">Skew</q-item>
        <q-item v-close-overlay @click.native="createNewBlock">SIFT</q-item>
      </q-collapsible>
      <q-btn
        self-end
        push
        color="primary"
        size="xl"
        label="Run"
      />
    </q-layout-drawer>
    <q-layout-header>
      <q-toolbar
        color="primary"
        :glossy="$q.theme === 'mat'"
        :inverted="$q.theme === 'ios'"
      >

        <q-toolbar-title>
          VPL-App
          <div slot="subtitle">Designed by us</div>
        </q-toolbar-title>
        <q-btn
          flat
          dense
          round
          @click="rightDrawerOpen = !rightDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn>
      </q-toolbar>
    </q-layout-header>

    <q-page-container ref="editor">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'
import PreviewWindow from '../components/layout/PreviewWindow.vue'

export default {
  name: 'MyLayout',
  components: {
    PreviewWindow
  },
  data () {
    return {
      rightDrawerOpen: this.$q.platform.is.desktop,
      typeOfComponent: 'block'
    }
  },
  methods: {
    openURL,
    createNewBlock: function () {
      var editorwindow = document.getElementById('blockcontainer')
      editorwindow.insertAdjacentHTML('beforeend', '<movableBlock class="movable" style="left:350px;top:50px;background-color:pink;height:100px;width:100px;">Some Text</movableBlock>')
    }
  }
}
</script>

<style>
.q-toolbar-title {
  text-align: center;
}

.layout-drawer {
  display: grid;
}
</style>
