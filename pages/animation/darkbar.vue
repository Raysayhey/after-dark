<template>
  <div class="main-container">
    <div class="overlay"></div>
    <div class="js-credits credits">
      <ul class="js-credit-container credit__container">
        <li v-for="n in item_count" :key="n" class="credit__item">{{n}}</li>
      </ul>
    </div>
  </div>
</template>
<style>
  .overlay {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    top: 0;
    animation: fade-in 5s;
    animation-fill-mode: forwards;
    animation-delay: 6s;
    background-color: #3e3e3e;
    opacity: 0;
    margin: 0 4%;
  }
  .credits {
    overflow: hidden;
  }
  .credit__container {
    font-size: 0;
    list-style-type: none;
    margin: 0 4%;
    padding: 0;
    position: relative;
  }

  .credit__item {
    background-color: black;
    height: calc(100vh / 28);
    transform: translateX(105%);
    width: 100%;
  }
  .credit__item.active {
    animation: slide-in 500ms forwards;
  }
  // Animation Keyframes

  @keyframes fade-in {
    100% {
      opacity: 1;
    }
  }

  @keyframes fade-in-out {
    0% {
      opacity: 0;
    }
    20% {
      opacity: 1;
    }
    80% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }

  @keyframes slide-in {
    100% {
      transform: translateX(0%);
    }
  }
</style>
<script>
  export default {
    transition: 'bounce',
    data() {
      return {
        item_count: 28
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
