<template>
  <div id="app">
    <div>
      <IPContainer></IPContainer>
    </div>
  </div>
</template>

<script>
import IPContainer from './components/IPContainer.vue'

export default {
  name: 'App',
  components: {
    IPContainer
  }
}
</script>

<style>
body{
  background-image: url("https://images.pexels.com/photos/125510/pexels-photo-125510.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=650&w=940");
  background-repeat: no-repeat
}
#app {

  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
