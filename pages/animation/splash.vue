<template>
  <div id="splash" :style="{ backgroundImage: `url(${splashUrl})` }">
  </div>
</template>
<style>
  #splash {
    position: absolute;
    top: 0px;
    bottom: 0px;
    left: 0px;
    right: 0px;
    height: 100vh;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    z-index: 10;
    overflow: hidden;
    opacity: 0;
    animation: fade-in-out 6s linear 1s forwards;
  }
</style>
<script>
  import splashUrl from '~/assets/img/logo.jpg'
  export default {
    transition: 'bounce',
    data() {
      return {
        splashUrl
      }
    },
    middleware: [
      function({ redirect }) {
        var animation_time = 6500;
        setTimeout(function() {
          var next_no = ++animation_no;
          if(next_no > animations.length)
            return true;
          console.log('animation_no>>>', next_no);
          return redirect(301, animations[next_no].path);
        }, animation_time);
      }
    ]
  }
</script>
