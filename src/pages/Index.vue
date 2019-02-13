<template>
  <q-page class="row justify-center items-center index-background">
    <img src="../assets/Wire_logo.svg" width="225px" height="225px">
    <div class="column">
      <q-btn label="New Project" class="margin-class bg-amber-9" v-on:click="newproject()"/>
      <q-btn label="Load Project" class="margin-class bg-amber-9"/>
      <q-btn label="First Steps" class="margin-class bg-amber-9"/>
      <q-btn label="Documentation" class="margin-class bg-amber-9"/>
    </div>
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
