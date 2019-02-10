<template>
  <q-layout view="lHh Lpr lFf">
    <block-selektor></block-selektor>
    <navbar></navbar>
    <q-page-container ref="editor">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { openURL } from 'quasar'
import BlockSelektor from '../components/layout/BlockSelektor.vue'
import Navbar from '../components/layout/Navbar'

export default {
  name: 'MyLayout',
  components: {
    BlockSelektor,
    Navbar
  },
  data () {
    return {
      typeOfComponent: 'block'
    }
  },
  methods: {
    openURL,
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
