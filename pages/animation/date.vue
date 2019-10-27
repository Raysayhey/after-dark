<template>
  <div class="main-container">
    <span class="date">{{date}}</span>
  </div>
</template>
<style>
  .date {
    position: fixed;
    top: 50%;
    right: 0;
    left: 0;
    -webkit-transform: translateY(-50%);
    -ms-transform: translateY(-50%);
    transform: translateY(-50%);
    font-size: calc(100vw / 10);
    text-align: center;
    letter-spacing: 0.125em;
    opacity: 0;
    animation: fade-in 4s;
    animation-fill-mode: forwards;
  }
</style>
<script>
  export default {
    data() {
      // var today = new Date();
      // var dd = String(today.getDate()).padStart(2, '0');
      // var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
      // var yyyy = today.getFullYear();

      // today = dd + '.' + mm + '.' + yyyy;

      var today = new Date();
      var dd = 1;
      var mm = 11;//January is 0!
      var yyyy = 2019;

      today = dd + '.' + mm + '.' + yyyy;
      var animation_date = today;
      return {
        date: animation_date
      }
    },
    middleware: [
      function({ redirect }) {
        var animation_time = 2000;
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
