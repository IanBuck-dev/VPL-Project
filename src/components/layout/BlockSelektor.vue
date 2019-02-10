<template>
  <q-layout-drawer
    row
    side="right"
    v-model="rightDrawerOpen"
    :content-class="$q.theme === 'mat' ? 'bg-grey-9' : null"
    class="layout-drawer"
  >
      <previewWindow></previewWindow>
      <div id="spacer" />
      <q-collapsible group="layoutMenu" link icon="add_circle_outline" label="Select new Blocks" dark>
        <q-collapsible group="drawerMenu" link icon="tune" label="Pre-Processing" dark>
            <q-item class="menu-button" @click.native="createNewBlock('Edge Extraction', 2)" >Edge Extraction</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Denoising', 2)">Denoising</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Blur Reduction', 2)">Blur Reduction</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Sharpening', 2)">Sharpening</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Brightness', 2)">Brightness</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Converting Color Spaces', 2)">Converting Color Spaces</q-item>
        </q-collapsible>
        <q-item-separator class="separator" />
        <q-collapsible icon="subject" group="drawerMenu" link dark indent label="Line Segmentation">
            <q-item class="menu-button" @click.native="createNewBlock('Text Split', 2)">Text Split</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Picture Split', 2)">Picture Split</q-item>
        </q-collapsible>
        <q-item-separator class="separator" />
        <q-collapsible icon="visibility" group="drawerMenu" link dark indent label="Optical Character Recognition">
            <q-item class="menu-button" @click.native="createNewBlock('Word and Char Processing', 3)">Word and Character Processing</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Skew', 3)">Skew</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('SIFT', 3)">SIFT</q-item>
        </q-collapsible>
        <q-item-separator class="separator" />
        <q-collapsible icon="shuffle" group="drawerMenu" link dark indent label="Scale-Invariant Feature Transform">
            <q-item class="menu-button" @click.native="createNewBlock('Scale-space Extrema Detection', 3)">Scale-space Extrema Detection</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Keypoint Localization', 3)">Keypoint Localization</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Orientation Assignment', 3)">Orientation Assignment</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Keypoint Descriptor', 3)">Keypoint Descriptor</q-item>
        </q-collapsible>
        <q-item-separator class="separator" />
        <q-collapsible icon="shuffle" group="drawerMenu" link dark indent label="Custom Blocks">
            <q-item class="menu-button" @click.native="createNewBlock('Scale-space Extrema Detection', 3)">Scale-space Extrema Detection</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Keypoint Localization', 3)">Keypoint Localization</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Orientation Assignment', 3)">Orientation Assignment</q-item>
            <q-item class="menu-button" @click.native="createNewBlock('Keypoint Descriptor', 3)">Keypoint Descriptor</q-item>
        </q-collapsible>
      </q-collapsible>
      <q-item-separator class="separator" />
      <q-collapsible group="layoutMenu" link icon="add_circle_outline" label="Select Procedures" dark>
        <q-item class="menu-button" @click.native="createNewBlock('Ancient Egypt Scripts', 3)">Ancient Egypt Scripts</q-item>
        <q-item class="menu-button" @click.native="createNewBlock('Greek Stone Plates', 3)">Greek Stone Plates</q-item>
        <q-item class="menu-button" @click.native="createNewBlock('Arabic Scripts', 3)">Arabic Scripts</q-item>
        <q-item class="menu-button" @click.native="createNewBlock('Nordic Artefacts', 3)">Nordic Artefacts</q-item>
      </q-collapsible>
      <q-btn id="run-btn"
        self-end
        push
        color="light"
        size="xl"
        label="Run"
      />
    </q-layout-drawer>
</template>

<script>
import PreviewWindow from '../layout/PreviewWindow.vue'

export default {
  name: 'BlockSelektor',
  components: {
    PreviewWindow
  },
  data () {
    return {
      setWidth: 200,
      rightDrawerOpen: this.$q.platform.is.desktop
    }
  },
  methods: {
    createNewBlock: function (name, type) {
      this.$root.$emit('block-created', name, type)
      this.notifyCreatedBlock(name, type)
      console.log(name + ' ' + type)
    },
    notifyCreatedBlock: function (name, type) {
      this.$q.notify({
        message: 'You just created a new block: ' + name + ' of type ' + type + '!',
        position: 'bottom-left',
        color: 'positive'
      })
    }
  }
}
</script>

<style>
</style>
