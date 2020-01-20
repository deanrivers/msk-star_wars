<template>
  <div id="app">
    <api/>
  </div>
</template>

<script>

import api from './components/api.vue'


export default {
  name: 'app',
  components: {
    api
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
