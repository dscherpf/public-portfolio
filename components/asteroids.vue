<template lang="html">
  <div class="wrap">

    <div class="neo-list">
      <div class="list-title">
        <h2>Near Earth Objects</h2>
      </div>
      <div class="list-filters">
        <div class="filter-title">
          <h3>Filters:</h3>
        </div>
        <div class="filters">
          <div :class="{ active: 'alpha' == activeFilter}" class="filter" @click="reorderData('alpha', 'name')" >Alphabetical</div>
          <div :class="{ active: 'diameter' == activeFilter}" class="filter" @click="reorderData('diameter', 'estimated_diameter.meters.estimated_diameter_max')" >Max est. diameter</div>
          <div :class="{ active: 'date' == activeFilter}" class="filter" @click="reorderData('date', 'orbital_data.first_observation_date')" >First observation</div>
        </div>
      </div>
      <div class="neos">
        <div class="neo"
             v-for="(neo, index) in NEOs"
             :key="index"
             :class="{ active: neo.name == activeNEO}"
             @click="toggleActiveNEO(neo), animeValueColor()"
        >
        {{ index + 1 }}. {{ neo.name }}
        </div>
      </div>
    </div>

    <div class="data-sheet" :class="{ active: data != ''}">
      <div class="display">
        <div id="h"></div>
        <svg width="500px" height="280px" viewBox="0 0 501 279" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
            <!-- Generator: Sketch 51.3 (57544) - http://www.bohemiancoding.com/sketch -->
            <desc>Created with Sketch.</desc>
            <defs></defs>
            <g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
                <g id="Artboard-6" transform="translate(-30.000000, -34.000000)">
                    <g id="model" transform="translate(31.000000, 35.000000)">
                        <ellipse id="sun" fill="#EDB947" fill-rule="nonzero" cx="78.6573146" cy="138.5" rx="22.5450902" ry="22.5"></ellipse>
                        <!-- <ellipse id="orbit" stroke="#3F5065" fill-rule="nonzero" cx="245.991984" cy="138.5" rx="245.991984" ry="138.5"></ellipse> -->
                        <path id="orbit" d="M0,138.5a245.991984,138.5 0 1,0 491.983968,0a245.991984,138.5 0 1,0 -491.983968,0" ></path>
                        <!-- <ellipse id="h" fill="#C4C9D1" fill-rule="nonzero" cx="491.983968" cy="137.5" rx="8.01603206" ry="8.5"></ellipse> -->
                        <path d="M113.791804,139.25 L482.400581,139.25" id="perihelion" stroke="#3F5065" stroke-linecap="square" fill-rule="nonzero"></path>
                        <path d="M45.5243821,138.25 L12.5918504,138.25" id="aphelion" stroke="#3F5065" stroke-linecap="square" fill-rule="nonzero"></path>
                        <text id="peri-text" font-family="sans-serif" font-size="14" font-weight="bold" letter-spacing="1" fill="#3F5065">
                            <tspan x="227.480347" y="132">Perihelion distance</tspan>
                        </text>
                        <text id="peri-value" font-family="LucidaGrande-Bold, Lucida Grande" font-size="14" font-weight="bold" letter-spacing="1" fill="#3F5065">
                            <tspan x="227.480347" y="156">{{ peri_value }} AU</tspan>
                        </text>
                    </g>
                </g>
            </g>
        </svg>
      </div>
      <div class="attrs">
        <div class="attr">
          <div class="attr-name">Name:</div>
          <div class="attr-value">{{ data.name }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Absolute magnitude (H):</div>
          <div class="attr-value">{{ data.absolute_magnitude_h }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Estimated diameter:</div>
          <div v-if="data != ''" class="attr-value">{{ data.estimated_diameter.meters.estimated_diameter_min }} - {{ data.estimated_diameter.meters.estimated_diameter_max }} meters</div>
        </div>
        <div class="attr">
          <div class="attr-name">Potentially hazardous:</div>
          <div class="attr-value">{{ data.is_potentially_hazardous_asteroid }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Sentry object:</div>
          <div class="attr-value">{{ data.is_sentry_object }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Aphelion distance:</div>
          <div v-if="data != ''" class="attr-value">{{ data.orbital_data.aphelion_distance }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Perihelion distance:</div>
          <div v-if="data != ''" class="attr-value">{{ data.orbital_data.perihelion_distance }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Orbit class type:</div>
          <div v-if="data != ''" class="attr-value">{{ data.orbital_data.orbit_class.orbit_class_type }}</div>
        </div>
        <div class="attr">
          <div class="attr-name">Observations used:</div>
          <div v-if="data != ''" class="attr-value">{{ data.orbital_data.observations_used }}</div>
        </div>

        <div class="info">
          <a v-if="`${data.nasa_jpl_url}` != ''" :href="`${ data.nasa_jpl_url }`" target="_blank">more info</a>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
// external
import _ from 'lodash';
import anime from 'animejs';
import axios from 'axios';

const NASA_KEY = process.env.NASA_KEY;

export default {
  data() {
    return {
      NEOs: [],
      activeFilter: '',
      activeNEO: '',
      data: '',
      peri_value: 0,
      // nasaKey: config.NASA_KEY,
    }
  },
  methods: {
    reorderData: function( name, attr ) {
      var NEOs = this.NEOs;
      this.NEOs = _.orderBy(NEOs, [ attr ], ['asc']);
      this.activeFilter = name;
    },
    setNEO: function() {

    },
    toggleActiveNEO: function( neo ) {
      var activeList = document.getElementsByClassName('neo active');
      var active = activeList[0];
      var activeData = neo;

      this.data = activeData;

      if ( this.activeNEO != neo.name ) {
        this.activeNEO = neo.name
      } else {
        this.activeNEO = null;
        active.classList.remove("active");
      };
      this.animeDisplay();
      // grab the updated perihelion distance
      var peri = this.data.orbital_data.perihelion_distance;
      // animate {{ peri_value }}
      anime({
        targets: this,
        peri_value: peri,
        duration: 1000,
      });
    },
    // animate color when NEO attribute values update
    animeValueColor: function() {
      anime({
        targets: '.attr-value',
        color: [
          { value: '#b1821a' },
          { value: '#c4c9d1' }
        ],
        duration: 500,
        easing: 'linear',
        // delay: 100
      });
    },
    // move the asteroid along it's path
    animeDisplay: function() {
      var path = anime.path('#model path');
      console.log('path');
      anime({
        targets: '#h',
        translateX: path('x'),
        translateY: path('y'),
        rotate: path('angle'),
        easing: 'linear',
        duration: 5000,
        loop: true,
      });
    }
  },
  created() {
  // API from https://api.nasa.gov/api.html#neows-browse
  axios.get('https://api.nasa.gov/neo/rest/v1/neo/browse?api_key=' + NASA_KEY)
  .then( response => {
    var neos = response.data.near_earth_objects;
    this.NEOs = neos;
  })
  .catch( error => {
    console.log(error);
  })
},
}
</script>

<style lang="scss">
@import "~/assets/scss/style.scss";

.wrap {
  display: flex;
  flex-direction: row;
}

.neo-list {
  margin-right: 1rem;
  border: 1px solid $dark_blue;
  padding: 1rem;
  text-align: left;

  .list-title {
    text-align: center;
    color: $light_gold;
    padding-bottom: .5rem;
  }

  .list-filters {
    display: flex;
    flex-direction: row;
    justify-content: space-between;

    border-top: 1px solid $dark_blue;
    border-bottom: 1px solid $dark_blue;
    padding: .5rem 0;

    & .filter-title {
      margin-right: 1rem;
      align-self: center;
    }
    & .filters {
      align-self: center;
    }
    & .filter {
      cursor: pointer;
      position: relative;
      padding: 0 .25rem;
      margin: .25rem 0;
    }
    & .filter::before {
      position: absolute;
      content: '';
      top: 0;
      left: 0;
      height: 100%;
      width: 1px;
      background-color: $light_gold;
      opacity: 0;
      z-index: -1;
    }
    & .filter:hover::before {
      opacity: 1;
    }
    & .filter.active::before {
      width: 100%;
      opacity: 1;

      -webkit-transition: width $n1;
      transition: width $n1;
    }
  }

  .neos {
    padding-top: 1rem;
  }

  & .neo {
    cursor: pointer;
  }
  & .neo.active {
    color: $light_gold;
  }
}

.data-sheet {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  border: 0px solid $dark_blue;
  padding: 0rem;
  text-align: left;
  width: 0px;
  // overflow: hidden;
  max-height: 580px;

  & .display {
    opacity: 0;
    transform: translateY(10px);
    align-self: center;
    z-index: -1;
  }
  & #h {
    width: 10px;
    height: 10px;
    background-color: $light_grey;
    border-radius: 100%;
  }
  & .attr {
    opacity: 0;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    border-bottom: 1px solid $dark_blue;
    transform: translateY(10px);
  }
  & .attr-name {
    margin-right: 1rem;
  }
  & .attr-value {}
  & .info {
    text-align: center;
    opacity: 0;
    transform: translateY(10px);
  }
  &.active {
    width: 560px;
    padding: 1rem;
    border: 1px solid $light_gold;

    -webkit-transition: all $n1;
    transition: all $n1;

    .attr, .info, .display {
      opacity: 1;
      transform: translateY(0px);

      -webkit-transition: all $n1;
      transition: all $n1;
      transition-delay: $n1;
    }
  }
}

</style>
