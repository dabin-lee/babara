<template>
  <the-header></the-header>
  <the-body></the-body>
</template>

<script>
import TheBody from './layouts/TheBody.vue'
import TheHeader from './layouts/TheHeader.vue'

export default {
  name: 'App',
  components: {
    TheHeader,
    TheBody
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
  margin-top: 60px;
}
</style>
