<template>
  <div id="app">
    <the-header />
    <the-body />
  </div>
</template>

<script>
import TheBody from './components/TheBody.vue'
import TheHeader from './components/TheHeader.vue'

export default {
  name: 'app',
  components: {
    TheBody,
    TheHeader,
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,600&display=swap');
@import url('style/helpers/index.css');

* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
