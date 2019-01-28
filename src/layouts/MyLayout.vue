<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-drawer
      row
      side="right"
      v-model="rightDrawerOpen"
      :content-class="$q.theme === 'mat' ? 'bg-grey-9' : null"
      class="layout-drawer"
    >
      <previewWindow></previewWindow>
      <div id="spacer" />
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
      <q-btn id="run-btn"
        self-end
        push
        color="light"
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
            <q-item>
              <q-item-side icon="create_new_folder" inverted color="light" />
              <q-item-main>
                <q-item-tile label v-on:click="newproject()">Start new Project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item>
              <q-item-side icon="folder" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Open project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
              <q-item-side icon="save" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Save project</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-list-header inset>Recent projects</q-list-header>
            <q-item>
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
            <q-item>
              <q-item-side icon="note_add" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Import document</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item>
              <q-item-side icon="save_alt" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Export document</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-list-header inset>Recently used documents</q-list-header>
            <q-item>
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
            <q-item>
              <q-item-side icon="photo_size_select_small" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Select Area</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
                <q-item>
              <q-item-side icon="rotate_right" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Rotate 90°</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
              <q-item-side icon="no_sim" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Cut</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
              <q-item-side icon="file_copy" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Copy</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
              <q-item-side icon="file_copy" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Paste</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
              <q-item-side icon="call_split" inverted color="light" />
              <q-item-main>
                <q-item-tile label>Separate Page</q-item-tile>
              </q-item-main>
              <q-item-side right icon="info" color="amber" />
            </q-item>
            <q-item-separator inset />
            <q-item>
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
          Wire©
          <div slot="subtitle">Designed in Germany</div>
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
    createNewBlock: function (name, type) {
      this.$root.$emit('block-created', name, type)
      console.log(name + ' ' + type)
    },
    newproject: function () {
      this.$root.$emit('new-project')
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

#spacer {
  height: 50px;
}

.separator {
  margin: 20px 0;
}

.menu-button {
  transition: background-color 0.25s;
}

.menu-button:hover {
  background-color: gray;
}

.menu-button:active {
  background-color: rgb(16, 245, 16);
}

#run-btn {
  color: #000 !important;
  margin: 30%;
  font-size: 1em !important;
  padding: 5px 40px;
}
</style>
