<template>
  <q-page class="column justify-center items-center index-background">
    <img src="../assets/Wire_logo.svg" width="200px" height="200px">
    <q-btn label="New Project" class="margin-class bg-amber-9" v-on:click="newproject()"/>
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

  .index-background {
    background: linear-gradient(45deg, #45484d 0%,#000000 100%);
  }
</style>
