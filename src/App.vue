<template>
  <div id="app">
    <ReportCard msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import ReportCard from './components/ReportCard.vue'

export default {
  name: 'app',
  components: {
    ReportCard
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
}
</style>
