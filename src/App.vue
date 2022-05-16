<template>
<div> 
  <!-- changed the logo -->
  <img alt="JG logo" src="https://upload.jln.pw/favion-cropped.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>
<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
/* changed the default backgroud color */
body{
  background-color: #9d959585;
}
/* text field input color */
input[type="text"] {
  background: #7fffd4;
}
</style>
