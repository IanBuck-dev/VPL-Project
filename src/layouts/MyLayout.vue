<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-header>
      <!-- First row of header is a QToolbar -->
      <q-toolbar>
        <!-- leftDrawerOpen is a model attached to left side drawer below -->
        <q-btn flat dense round @click="leftDrawerOpen = !leftDrawerOpen" aria-label="left Menu">
          <q-icon name="menu"/>
        </q-btn>
        <q-toolbar-title>
          Image Document Processing Visual Programming App
          <span slot="subtitle">Project Mock Up</span>
        </q-toolbar-title>
        <!-- rightDrawerOpen is a model attached to right side drawer below -->
        <q-btn flat dense round @click="rightDrawerOpen = !rightDrawerOpen" aria-label="right Menu">
          <q-icon name="menu"/>
        </q-btn>
      </q-toolbar>
    </q-layout-header>

    <q-layout-drawer
      side="left"
      v-model="leftDrawerOpen"
      :content-class="$q.theme === 'mat' ? 'bg-grey-2' : null"
    >
      <q-list no-border link inset-delimiter>
        <q-list-header>Essential Links</q-list-header>
        <q-item @click.native="openURL('http://quasar-framework.org')">
          <q-item-side icon="school"/>
          <q-item-main label="Docs" sublabel="quasar-framework.org"/>
        </q-item>
        <q-item @click.native="openURL('https://github.com/quasarframework/')">
          <q-item-side icon="code"/>
          <q-item-main label="GitHub" sublabel="github.com/quasarframework"/>
        </q-item>
        <q-item @click.native="openURL('https://discord.gg/5TDhbDg')">
          <q-item-side icon="chat"/>
          <q-item-main label="Discord Chat Channel" sublabel="https://discord.gg/5TDhbDg"/>
        </q-item>
        <q-item @click.native="openURL('http://forum.quasar-framework.org')">
          <q-item-side icon="record_voice_over"/>
          <q-item-main label="Forum" sublabel="forum.quasar-framework.org"/>
        </q-item>
        <q-item @click.native="openURL('https://twitter.com/quasarframework')">
          <q-item-side icon="rss feed"/>
          <q-item-main label="Twitter" sublabel="@quasarframework"/>
        </q-item>
      </q-list>
    </q-layout-drawer>

    <q-layout-drawer
      side="right"
      v-model="rightDrawerOpen"
      content-class="bg-grey-1"
      :content-style="{
        padding: '20px'
      }"
      id="mockMenu"
    >
      <q-card style="width: 100px">
        <q-card-title>Preview</q-card-title>
        <q-card-separator/>
        <q-card-media>
          <img src="../assets/mark-rasmuson-108148-unsplash.jpg">
        </q-card-media>
        <q-card-actions>
          <q-slider v-model="selectedValue" :min="0" :max="10" :step="2" label snap/>
        </q-card-actions>
      </q-card>
      <q-btn label="Pre-Processing">
        <q-popover>
          <q-list no-border link inset-delimiter>
            <q-item v-close-overlay @click.native="doSomething">Edge Extraction</q-item>
            <q-item v-close-overlay @click.native="doSomething">Denoising</q-item>
            <q-item v-close-overlay @click.native="doSomething">Blur Reduction</q-item>
            <q-item v-close-overlay @click.native="doSomething">Sharpening</q-item>
            <q-item v-close-overlay @click.native="doSomething">Brightness</q-item>
            <q-item v-close-overlay @click.native="doSomething">Converting Color Spaces</q-item>
          </q-list>
        </q-popover>
      </q-btn>
      <q-btn label="Line Segmentation">
        <q-popover>
          <q-list separator link>
            <q-item v-close-overlay @click.native="doSomething">Floodfill Segmentation</q-item>
            <q-item v-close-overlay @click.native="doSomething">Sequential Segmentation</q-item>
            <q-item v-close-overlay @click.native="doSomething">Text Split</q-item>
            <q-item v-close-overlay @click.native="doSomething">Picture Split</q-item>
          </q-list>
        </q-popover>
      </q-btn>
      <q-btn label="Optical Character Recognition">
        <q-popover>
          <q-list separator link>
            <q-item v-close-overlay @click.native="doSomething">Word and Character Processing</q-item>
            <q-item v-close-overlay @click.native="doSomething">Skew</q-item>
          </q-list>
        </q-popover>
      </q-btn>
      <q-btn label="Scale-Invariant Feature Transform">
        <q-popover>
          <q-list separator link>
            <q-item v-close-overlay @click.native="doSomething">Scale-space Extrema Detection</q-item>
            <q-item v-close-overlay @click.native="doSomething">Keypoint Localization</q-item>
            <q-item v-close-overlay @click.native="doSomething">Orientation Assignment</q-item>
            <q-item v-close-overlay @click.native="doSomething">Keypoint Descriptor</q-item>
          </q-list>
        </q-popover>
      </q-btn>
    </q-layout-drawer>

    <q-page-container>
      <router-view/>
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from "quasar";

export default {
  name: "MyLayout",
  data() {
    return {
      leftDrawerOpen: this.$q.platform.is.desktop
    };
  },
  methods: {
    openURL
  }
};
</script>

<style>
  #mockMenu > * {
    margin: 10px;
  }
</style>
