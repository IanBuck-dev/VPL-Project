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
    <q-layout-header class="row justify-start">
      <q-toolbar
        color="dark"
        :glossy="$q.theme === 'ios'"
        :inverted="$q.theme === 'ios'"
        >
      <q-btn-group>
        <q-btn-dropdown color="dark" label="Project" class="q-mr-md">
          <!-- dropdown content goes here -->
          <q-list link>
            <q-item v-close-overlay>
              <q-item-side icon="create_new_folder" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Start new project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item v-close-overlay>
              <q-item-side icon="folder" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Open project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="save" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Save project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-list-header inset>Recent projects</q-list-header>
            <q-item v-close-overlay>
              <q-item-side icon="access_time" inverted color="light"/>
              <q-item-main>
                <q-item-tile label>Project_XYZ</q-item-tile>
                <q-item-tile sublabel> (December 14, 2018)</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown color="dark" label="Document" class="q-mr-md">
          <!-- dropdown content goes here -->
          <q-list link>
            <q-item v-close-overlay>
              <q-item-side icon="note_add" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Import document</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item v-close-overlay>
              <q-item-side icon="save_alt" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Export document</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-list-header inset>Recently used documents</q-list-header>
            <q-item v-close-overlay>
              <q-item-side icon="access_time" inverted color="light"/>
              <q-item-main>
                <q-item-tile label>Document_XYZ</q-item-tile>
                <q-item-tile sublabel> (December 14, 2018)</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
          </q-list>
        </q-btn-dropdown>
        <q-btn-dropdown color="dark" label="Workspace" class="q-mr-md">
          <!-- dropdown content goes here -->
          <q-list link>
            <q-item v-close-overlay>
              <q-item-side icon="photo_size_select_small" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Select Area</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item v-close-overlay>
              <q-item-side icon="rotate_right" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Rotate 90°</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="no_sim" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Cut</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="file_copy" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Copy</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="file_copy" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Paste</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="call_split" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Separate Page</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item v-close-overlay>
              <q-item-side icon="merge_type" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Merge Pages</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
          </q-list>
        </q-btn-dropdown>
          <q-btn-dropdown color="dark" label="History" class="q-mr-md" />
      </q-btn-group>
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
