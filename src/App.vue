<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <videoPlay></videoPlay>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import videoPlay from './components/videoPlay.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    videoPlay
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
