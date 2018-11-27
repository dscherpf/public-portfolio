<template>
  <section class="main">
    <div class="nav">
      <h1 class="title">
        Dylan Scherpf
      </h1>
      <!-- <h2 class="subtitle">
        Dylan Scherpf
      </h2> -->
      <div class="nav-list">
        <div class="nav-item"
             v-for="(item, index) in navItems"
             v-bind:key="index"
             v-on:click="toggleActiveItem(item)"
             :class="{ active: item.name == activeNavItem}"
             >
          <h2
              @mouseover="animeIcon( `a${index}`, 0 )"
              @mouseleave="animeIcon( `a${index}`, -40)"
              >
          {{ item.name }}
          </h2>
          <div :class="`nav-arrow a${index}`" >

            <svg v-if="`${ item.name }` !== activeNavItem" width="20px" height="21px" viewBox="0 0 20 21" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <!-- Generator: Sketch 51.3 (57544) - http://www.bohemiancoding.com/sketch -->
                <desc>Created with Sketch.</desc>
                <defs></defs>
                <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                    <g id="Artboard-3" transform="translate(-416.000000, -350.000000)" fill-rule="nonzero">
                        <g id="down-arrow" transform="translate(416.000000, 350.000000)">
                            <polyline id="L2" stroke="#B1821A" stroke-width="1" stroke-linecap="square" points="18.3103448 10.5 10.0344828 21 10.0344828 0"></polyline>
                            <polyline id="L1" stroke="#B1821A" stroke-width="1" stroke-linecap="square" transform="translate(5.827586, 10.500000) scale(-1, 1) translate(-5.827586, -10.500000) " points="9.96551724 10.5 1.68965517 21 1.68965517 0"></polyline>
                        </g>
                    </g>
                </g>
            </svg>

            <svg v-if="`${ item.name }` == activeNavItem" width="20px" height="21px" viewBox="0 0 20 21" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
                <!-- Generator: Sketch 51.3 (57544) - http://www.bohemiancoding.com/sketch -->
                <desc>Created with Sketch.</desc>
                <defs></defs>
                <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                    <g id="Artboard-3" transform="translate(-441.000000, -350.000000)" fill-rule="nonzero">
                        <g id="close" transform="translate(441.000000, 350.000000)">
                            <path d="M1,20 L19.5,0.5" id="L2" stroke="#B1821A" stroke-linecap="square"></path>
                            <path d="M19,20 L0.5,0.5" id="L1" stroke="#B1821A" stroke-linecap="square"></path>
                        </g>
                    </g>
                </g>
            </svg>

          </div>
        </div>

      </div>
    </div>
    <div class="container">
      <about v-if="activeNavItem == 'about'"/>
      <work v-if="activeNavItem == 'work'"/>
      <asteroids v-if="activeNavItem == 'asteroids'"/>
      <sol v-if="activeNavItem == null"/>
    </div>
  </section>
</template>

<script>
// content
import about from '~/components/about.vue'
import work from '~/components/work.vue'
import asteroids from '~/components/asteroids.vue'
// svg
import sol from '~/components/sol.vue'
// external
import anime from 'animejs'

export default {
  components: {
    about,
    work,
    asteroids,
    sol
  },
  data() {
    return {
      assetPath: '~/assets/',
      arrow: '~/assets/images/arrow.svg',
      duration: 250,
      activeNavItem: null,
      navItems: [
        { name: 'work' },
        { name: 'asteroids' },
        { name: 'about' }
      ],
    }
  },
  methods: {
    animeIcon: function( target, offset ) {
      // prevent animations from getting stuck midway on quick mouseover/mouseleave
      anime.remove('.' + target + ' #L1');
      anime.remove('.' + target + ' #L2');
      // arrow stroke animation
      anime({
        targets: [ '.' + target + ' #L1', '.' + target + ' #L2'],
        strokeDashoffset: {
          value: offset,
          duration: this.duration,
          easing: 'linear',
        },
        strokeDasharray: {
          value: '40 40',
          duration: this.duration,
          easing: 'linear'
        }
      });
    },
    toggleActiveItem: function( item ) {
      var activeList = document.getElementsByClassName('nav-item active');
      var active = activeList[0];

      if ( this.activeNavItem != item.name ) {
        this.activeNavItem = item.name
      } else {
        this.activeNavItem = null;
        active.classList.remove("active");
      }
    },
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/style.scss";

body {
  background-color: $dark_grey;
  font-family: 'Raleway', sans-serif;
}

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 6rem 2rem 2rem;

  @include desktop {
    padding: 4rem 2rem 2rem;
  }
}

.title {
  font-family: 'Roboto', sans-serif;
  display: inline-block;
  font-weight: 300;
  font-size: 36px;
  color: $light_gold;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.subtitle {
  font-weight: 300;
  font-size: 20px;
  color: $white;
  word-spacing: 5px;
  padding-bottom: 15px;
  text-transform: uppercase;
}

.links {
  padding-top: 15px;
}

.nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 4rem;
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  background-color: $dark_grey;
  border-bottom: 1px solid $dark_blue;
  z-index: 1000;

  @include desktop {
    min-height: 3rem;
  }

  .title {
    position: absolute;
    top: .25rem;
    left: .5rem;
  }

  &-list {
    display: flex;
    flex-direction: row;
  }

  &-item {
    position: relative;
    align-self: flex-end;
    margin: 0 1rem;
  }
  &-item h2 {
    color: $dark_blue;
    cursor: pointer;

    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-fill-color: transparent;
    background-image: linear-gradient( $dark_blue 24px, $light_gold 24px );
    background-size: 100% 24px;
    background-position: bottom;

    -webkit-transition: all $n1;
    transition: all $n1;
  }
  &-item h2:hover {
    background-size: 100% 48px;
    -webkit-transition: all $n1;
    transition: all $n1;
  }
  &-item h2::after {
    display: block;
    position: absolute;
    content: '';
    width: 100%;
    // bottom: -1px;
    border-bottom: 1px solid $light_gold;
    transform: scaleX(0);
    transition: transform 250ms linear;
  }
  &-item.active h2::after {
    transform: scaleX(1);
    transition: transform 250ms linear;
  }
  &-item.active {

    h2 {
      background-size: 100% 48px;
    }
    // .nav-arrow {
      // display: none;
    // }
  }

  .nav-arrow {
    position: absolute;
    bottom: -28px;
    width: 100%;
    pointer-events: none;
    display: flex;
    flex-direction: row;
    justify-content: center;

    svg {
      // align-self: center;
    }
  }
  #L1, #L2 {
    stroke-dasharray: 40 40;
    stroke-dashoffset: -40;
  }
}
</style>
