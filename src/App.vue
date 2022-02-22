<template>
  <div id="app">
    <div>Machine Learning</div>
     <MachineLearning msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import MachineLearning from './components/MachineLearning.vue'

export default {
  name: 'App',
  components: {
    MachineLearning
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
