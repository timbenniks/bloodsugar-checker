<template>
  <bs></bs>
</template>

<script>
import bs from './components/bs';

export default {
  name: 'app',
  components: {
    bs
  }
}
</script>

<style>
body {
  font-family: 'Source Sans Pro', 'Helvetica Neue', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
  color: #2c3e50;
  line-height: 1.8;
  font-size: 100%;
  background: #f6f6f6;
}

main {
  max-width: 500px;
  margin: 0 auto;
}
</style>
