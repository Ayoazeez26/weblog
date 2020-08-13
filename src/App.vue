<template>
  <div id="app">
    <Navbar />
    <Check />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Check from './components/Check.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    Check
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
</style>
