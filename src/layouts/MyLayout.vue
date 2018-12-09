<template>
  <q-layout view="lHh Lpr lFf">
    <q-layout-drawer
      row
      side="right"
      v-model="leftDrawerOpen"
      :content-class="$q.theme === 'mat' ? 'bg-grey-2' : null"
      class="layout-drawer"
    >
      <previewWindow></previewWindow>
      <q-collapsible indent label="Menu">
        <p>Some text</p>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Menu">
        <p>Some text</p>
      </q-collapsible>
      <q-item-separator />
      <q-collapsible indent label="Menu">
        <p>Some text</p>
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
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn>

        <q-toolbar-title>
          VPL-App
          <div slot="subtitle">Designed by us</div>
        </q-toolbar-title>
      </q-toolbar>
    </q-layout-header>

    <q-toolbar
        color="primary"
        :glossy="$q.theme === 'mat'"
        :inverted="$q.theme === 'ios'"
      >
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
        >
          <q-icon name="menu" />
        </q-btn>

        <q-toolbar-title>
          VPL-App
          <div slot="subtitle">Designed by us</div>
        </q-toolbar-title>
      </q-toolbar>

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
      leftDrawerOpen: this.$q.platform.is.desktop
    }
  },
  methods: {
    openURL
  }
}
</script>

<style>
.layout-drawer {
  display: grid;
}
</style>
