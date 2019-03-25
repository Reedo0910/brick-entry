<template>
  <div id="app">
    <dial></dial>
  </div>
</template>

<script>
  import Dial from './components/Dial.vue'

  export default {
    name: 'app',
    components: {
      Dial
    },
    beforeMount() {
      document.body.addEventListener('touchstart', function () { });
    },
    beforeDestroy() {
      document.body.removeEventListener('touchstart', function () { });
    }
  }
</script>

<style>
  body {
    background-color: #222;
    width: 100vw;
    height: 100vh;
    position: relative;
    overflow: hidden;
    margin: 0;
    padding: 0;
  }
</style>
