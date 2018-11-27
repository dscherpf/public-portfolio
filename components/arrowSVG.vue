<template lang="html">
  <svg width="20px" height="21px" viewBox="0 0 20 21" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
      <!-- Generator: Sketch 51.3 (57544) - http://www.bohemiancoding.com/sketch -->
      <desc>Created with Sketch.</desc>
      <defs></defs>
      <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
          <g id="Artboard-3" transform="translate(-416.000000, -350.000000)" fill-rule="nonzero">
              <g id="down-arrow" transform="translate(416.000000, 350.000000)">
                  <rect id="Rectangle-2" fill-opacity="0" fill="#D8D8D8" x="0" y="0" width="20" height="21"></rect>
                  <polyline id="L2" stroke="#B1821A" stroke-width="1" stroke-linecap="square" points="18.3103448 10.5 10.0344828 21 10.0344828 0"></polyline>
                  <polyline id="L1" stroke="#B1821A" stroke-width="1" stroke-linecap="square" transform="translate(5.827586, 10.500000) scale(-1, 1) translate(-5.827586, -10.500000) " points="9.96551724 10.5 1.68965517 21 1.68965517 0"></polyline>
              </g>
          </g>
      </g>
  </svg>
</template>

<script>
export default {
  data() {
    return {
      duration: 300,
    }
  },
  methods: {
    animeIcon: function() {
      console.log("animejs");
      // prevent animations from getting stuck midway on quick mouseover/mouseleave
      // anime.remove(blueTarget);
      // anime.remove(whiteTarget);
      // blue line animation
      anime({
        targets: ['#L1', '#L2'],
        strokeDashoffset: {
          value: 20,
          duration: this.duration,
          easing: 'linear',
        },
        strokeDasharray: {
          value: '20 20',
          duration: this.duration,
          easing: 'linear'
        }
      });
    }
  }
}
</script>

<style lang="scss">
</style>
