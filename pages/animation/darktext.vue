<template>
  <div class="main-container">
    <div id="jsi-bg" class="bg">
      <ul id="jsi-animators--horizontal-lines" class="horizontal-lines"></ul>
      
      <div id="jsi-animators--movie-title" class="movie-title"></div>
    </div>
  </div>
</template>
<style>
  .bg {
    width: 100vw;
    height: 100vh;
    background-color: #2B292B;
  }
  .bg > ul > li {
    background-color: #010001;
  }
  .bg > ul.horizontal-lines > li {
    float: right;
    clear: both;
    width: 1px;
    margin-top: calc(100vh / (15 * 2));
    height: calc(100vh / (15 * 2));
    transition: width 1000ms linear;
  }
  .bg > ul.horizontal-lines > li.is-animating--right-to-left {
    width: 100vw;
  }
  .bg > ul.horizontal-lines > li.is-animating--left-to-right {
    float: left;
    width: 0vw;
  }

  .movie-title > div {
    position: fixed;
    top: 50%;
    right: 0;
    left: 0;
    margin-top: -10vh;
    font-size: calc(100vh / (15 * 2) * 5);
    text-align: center;
    letter-spacing: 0.125em;
    -webkit-transform: translate(100vw);
            transform: translate(100vw);
    transition: -webkit-transform 500ms linear;
    transition: transform 500ms linear;
    transition: transform 500ms linear, -webkit-transform 500ms linear;
  }
  .movie-title > div.is-animating--right-to-left {
    -webkit-transform: translate(0);
            transform: translate(0);
  }
  .movie-title > div.is-animating--as-crazy-left {
    margin-left: -0.25em;
  }
  .movie-title > div.is-animating--as-crazy-right {
    margin-left: 0.25em;
  }
  .movie-title > div:nth-child(1) {
    clip: rect(0vw, 100vw, calc(calc(100vh / (15 * 2) * 5) / 2.3), 0);
  }
  .movie-title > div:nth-child(2) {
    clip: rect(calc(calc(100vh / (15 * 2) * 5) / 2.4), 100vw, calc(calc(100vh / (15 * 2) * 5) / 1.5), 0);
  }
  .movie-title > div:nth-child(3) {
    clip: rect(calc(calc(100vh / (15 * 2) * 5) / 1.5), 100vw, calc(100vh / (15 * 2) * 5), 0);
  }
</style>
<script>
  var Credits;
  $(function() {
    /**
     * constants
     */
    const classNames = {
      isAnimating: 'is-animating',
      shouldShown: 'should-shown',
      rightToLeft: 'is-animating--right-to-left',
      leftToRight: 'is-animating--left-to-right',
      crazyLeft: 'is-animating--as-crazy-left',
      crazyRight: 'is-animating--as-crazy-right'
    };
    const movieTitle = 'After Dark';
    const movieDivisionsLength = 3;
    const horizontalLinesLength = 15;

    Credits = class Credits {
      constructor() {
        /**
         * DOM elements
         */
        this.$bg = document.getElementById('jsi-bg');
        this.$animators = {
          horizontalLines: document.getElementById('jsi-animators--horizontal-lines'),
          movieTitle: document.getElementById('jsi-animators--movie-title')
        };
        this.prepareElements();
        this.startHorizontalLines();
      }
      prepareElements = () => {
        for (let i = 0; i < movieDivisionsLength; i++) {
          this.$animators.movieTitle.insertAdjacentHTML('afterbegin', '<div>' + movieTitle + '</div>');
        }
        
        for (let i = 0; i < horizontalLinesLength; i++) {
          this.$animators.horizontalLines.insertAdjacentHTML('afterbegin', '<li></li>');
        }
      }
      startHorizontalLines = () => {
        /**
         * set animationg marker
         */
        this.$bg.classList.add(classNames.isAnimating);
        
        /**
         * horizontal lines appearance
         */
        let animationOrder = [];
        for (let i = 0; i < horizontalLinesLength; i++) {
          animationOrder.push(i);
        }
        animationOrder = animationOrder.sort(() => {
          return Math.random() * 2 - 1;
        });
        let intervalCount = 0;
        const animateHorizontalLines = setInterval(() => {
          if (intervalCount > horizontalLinesLength) {
            clearInterval(animateHorizontalLines);
          }
          const $target = this.$animators.horizontalLines.querySelectorAll('li')[animationOrder[intervalCount]];
          if ($target) $target.classList.add(classNames.rightToLeft);
          intervalCount++;
        }, 250);

        /**
         * movie title appearance
         */
        let movieTitleAnimateOrder = [0, 2, 1];
        let movieTitleIntervalCount = 0;
        setInterval(() => {
          const animateMovieTitle = setInterval(() => {
            if (intervalCount > movieDivisionsLength) {
              clearInterval(animateMovieTitle);
            }
            const $target = this.$animators.movieTitle.querySelectorAll('div')[movieTitleAnimateOrder[movieTitleIntervalCount]];
            if ($target) $target.classList.add(classNames.rightToLeft);
            movieTitleIntervalCount++;
          }, 250);
        }, 1250);

        /**
         * logo breaking --first
         */
        setTimeout(() => {
          this.$animators.movieTitle.querySelectorAll('div')[1].classList.add(classNames.crazyLeft);
          this.$animators.movieTitle.querySelectorAll('div')[2].classList.add(classNames.crazyRight);
        }, 5000);

        /**
         * horizontal lines disappearance
         */
        setTimeout(() => {
          let intervalCount = 0;
          const animateHorizontalLines = setInterval(() => {
            if (intervalCount > horizontalLinesLength) {
              clearInterval(animateHorizontalLines);
            }
            const $target = this.$animators.horizontalLines.querySelectorAll('li')[animationOrder[intervalCount]];
            if ($target) {
              $target.classList.remove(classNames.rightToLeft);
              $target.classList.add(classNames.leftToRight); 
            }
            intervalCount++;
          }, 50);
        }, 5500);

        /**
         * logo breaking --second
         */
        setTimeout(() => {
          this.$animators.movieTitle.querySelectorAll('div')[1].classList.remove(classNames.crazyLeft);
          this.$animators.movieTitle.querySelectorAll('div')[1].classList.add(classNames.crazyRight);
          this.$animators.movieTitle.querySelectorAll('div')[2].classList.remove(classNames.crazyRight);
          this.$animators.movieTitle.querySelectorAll('div')[2].classList.add(classNames.crazyLeft);
          
          this.$bg.classList.remove(classNames.isAnimating);
        }, 6000);
      }
    };
  });
  export default {
    transition: 'bounce',
    async asyncData() {
      setTimeout(() => {
        new Credits();
      }, 500);
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
    ],
  }
</script>
