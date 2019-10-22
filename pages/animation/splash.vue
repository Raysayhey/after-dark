<template>
  <div id="splash" :style="{ backgroundImage: `url(${splashUrl})` }">
    <div class="title">
      <h1>Animation is Fun!</h1>
    </div>
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
    background-size: contain;
    background-position: center;
    background-repeat: no-repeat;
    z-index: 10;
    overflow: hidden;
    animation: fadeinout 6s linear 1s forwards;
  }
  .title {
    position: fixed;
    bottom: -60px;
    left: 0;
    right: 0;
    text-align: center;
    height: fit-content;
    animation: animatebottom 2s linear 1s forwards;
  }
  @keyframes fadeinout {
    from {
      visibility: visible;
      opacity: 1;
      transition: opacity 2s linear;
    }
    to {
      visibility: hidden;
      opacity: 0;
      transition: visibility 0s 2s, opacity 2s linear;
    }
  }
  @keyframes animatebottom {
    from {top: 100%;}
    to {top: 10%;}
  }
</style>
<script>
  import splashUrl from '~/assets/img/splash.gif'
  export default {
    transition: 'bounce',
    data() {
      return {
        splashUrl
      }
    },
    middleware: [
      function({ redirect }) {
        var animation_time = 6000;
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
