<template>
  <q-page class="column justify-center items-center bg-dark">
    <img src="../assets/quasar-logo-full.svg" width="200px" height="200px">
    <q-btn label="New Project" class="margin-class bg-primary" v-on:click="newproject()"/>
  </q-page>
</template>

<style>
</style>

<script>

export default {
  name: 'PageIndex',
  methods: {
    newproject: function () {
      this.$router.push({path: 'editor'})
    }
  }
}

</script>

<style>
  .margin-class {
    margin: 10px;
  }
</style>
