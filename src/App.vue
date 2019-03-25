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

      // document.addEventListener('touchstart', function (event) {
      //   if (event.touches.length > 1) {
      //     event.preventDefault();
      //   }
      // });

      // let lastTouchEnd = 0;
      // document.addEventListener('touchend', function (event) {
      //   let now = (new Date()).getTime();
      //   if (now - lastTouchEnd <= 100) {
      //     event.preventDefault();
      //   }
      //   lastTouchEnd = now;
      // }, false);

      // document.addEventListener('gesturestart', function (event) {
      //   event.preventDefault();
      // });
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
