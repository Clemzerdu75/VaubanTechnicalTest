<template>
  <div id="app">
    <Main/>
  </div>
</template>

<script>
import Main from './components/Main.vue'

export default {
  name: 'app',
  components: {
    Main
  },
}
</script>

<style>
#app {
  font-family:  Helvetica, Arial, sans-serif;
  text-align: center;
  color: #f0f0f0;
}
</style>
