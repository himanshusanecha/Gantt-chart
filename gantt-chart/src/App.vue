<template>
  <div class="app">
    <ViewTimeline />
  </div>
</template>

<script>
import ViewTimeline from './components/ViewTimeline.vue'

export default {
  name: 'App',
  components: {
    ViewTimeline
  }
}
</script>

<style>
.app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 120px;
  margin-left: auto;
  margin-right: auto;
  width: 100vw;
  overflow-x: hidden;
}
</style>
