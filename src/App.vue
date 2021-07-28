<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Memos />
  </div>
</template>

<script>
import Memos from './components/Memos.vue';

export default {
  name: 'App',
  components: {
    Memos
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
