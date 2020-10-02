<template>
  <div id="app">
    <music></music>
  </div>
</template>

<script>
import Music from './components/Music.vue'

export default {
  name: 'App',
  components: {
    Music
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body{
  font-family: "Roboto Light",serif;
}
</style>
