<template>
  <Content class="content" />
</template>

<script>
import Content from './components/Content.vue'

export default {
  name: 'app',
  components: {
    Content,
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,500&display=swap');
@import url('style/helpers/index.css');

* {
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}

.content {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
