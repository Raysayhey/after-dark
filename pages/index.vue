<template>
  <div class="main-container"></div>
</template>
<script>
  export default {
    middleware: [
      function({ redirect }) {
        var animation_time = 1000;
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