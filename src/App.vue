<template>
  <div id="app">
    <ApiStuff/>
  </div>
</template>

<script>

import ApiStuff from './components/ApiStuff.vue';

export default {
  name: 'app',
  components: {
    ApiStuff
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(69, 75, 61);
  background: rgb(161, 153, 147);
}
</style>
