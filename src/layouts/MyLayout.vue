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
        <q-item v-close-overlay @click.native="doSomething">Edge Extraction</q-item>
        <q-item v-close-overlay @click.native="doSomething">Denoising</q-item>
        <q-item v-close-overlay @click.native="doSomething">Blur Reduction</q-item>
        <q-item v-close-overlay @click.native="doSomething">Sharpening</q-item>
        <q-item v-close-overlay @click.native="doSomething">Brightness</q-item>
        <q-item v-close-overlay @click.native="doSomething">Converting Color Spaces</q-item>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Line Segmentation">
        <q-item v-close-overlay @click.native="doSomething">Text Split</q-item>
        <q-item v-close-overlay @click.native="doSomething">Picture Split</q-item>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Optical Character Recognition">
        <q-item v-close-overlay @click.native="doSomething">Word and Character Processing</q-item>
        <q-item v-close-overlay @click.native="doSomething">Skew</q-item>
        <q-item v-close-overlay @click.native="doSomething">SIFT</q-item>
      </q-collapsible>
      <q-collapsible indent label="Scale-Invariant Feature Transform">
        <q-item v-close-overlay @click.native="doSomething">Scale-space Extrema Detection</q-item>
        <q-item v-close-overlay @click.native="doSomething">Keypoint Localization</q-item>
        <q-item v-close-overlay @click.native="doSomething">Orientation Assignment</q-item>
        <q-item v-close-overlay @click.native="doSomething">Keypoint Descriptor</q-item>
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

    <q-page-container>
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
      rightDrawerOpen: this.$q.platform.is.desktop
    }
  },
  methods: {
    openURL
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
