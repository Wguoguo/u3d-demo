<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <img alt="unity logo" class="unity-logo" src="./assets/unity-logo.jpg">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
    // const ref = this;
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  .unity-logo{
    width: 120px;
  }
}
</style>
