<template>
  <div class="main-container">
    <div class="overlay"></div>
    <div class="js-credits credits">
      <ul class="js-credit-container credit__container">
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
    animation: fade-in 4s;
    animation-fill-mode: forwards;
    animation-delay: 1s;
    background-color: #3e3e3e;
    opacity: 0;
    margin: 0;
  }
  .credits {
    overflow: hidden;
  }
  .credit__container {
    font-size: 0;
    list-style-type: none;
    margin: 0;
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

</style>
<script>
  var item_count = 28;
  var Credits;
  $(function() {
    Credits = class Credits {
      constructor($wrap) {
        this.$wrap = $wrap;
        this.$creditContainer = this.$wrap.find('.js-credit-container');
        this.creditInit();
      }

      creditInit() {
        var i, j, results;
        results = [];
        for (i = j = 1; j <= item_count; i = ++j) {
          results.push((i => {
            this.$creditContainer.append('<li class="credit__item"></li>');
            if (i === item_count) {
              return setTimeout(() => {
                return this.slideIn();
              }, 4000);
            }
          })(i));
        }
        return results;
      }

      slideIn() {
        var index, j, len, order, position, results;
        console.log('run');
        order = [4, 20, 0, 24, 6, 22, 12, 2, 16, 10, 18, 26, 14, 8];
        results = [];
        for (index = j = 0, len = order.length; j < len; index = ++j) {
          position = order[index];
          results.push(((index, position) => {
            var delay;
            delay = Math.random() * 500 * index + Math.random() * 500;
            return setTimeout(() => {
              return $('.credit__item').eq(position).addClass('active');
            }, delay);
          })(index, position));
        }
        return results;
      }
    };
  });
  export default {
    transition: 'bounce',
    async asyncData() {
      setTimeout(() => {
        return new Credits($('.js-credits'));
      }, 1000);
    },
    middleware: [
      function({ redirect }) {
        var animation_time = 10000;
        setTimeout(function() {
          var next_no = ++animation_no;
          if(next_no >= animations.length)
            return true;
          console.log('animation_no>>>', next_no);
          return redirect(301, animations[next_no].path);
        }, animation_time);
      }
    ]
  }
</script>
