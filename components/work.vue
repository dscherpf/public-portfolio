<template lang="html">
  <div class="work-samples">
    <div class="sample" v-for="(sample, index) in samples" v-bind:key="index">

      <a class="sample-title" :href="`${sample.link}`" target="_blank">{{ sample.name }}</a>

      <div class="attributes">
        <div class="attribute">
          <h4>Role:</h4> {{ sample.role }}
        </div>
        <div class="attribute">
          <h4>Project:</h4> <span v-html="`${ sample.description }`"></span>
        </div>
        <div class="attribute">
          <h4>Recent Updates:</h4> <span v-html="`${ sample.recent }`"></span>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      samples: [
        { name: 'Morgan Stanley', link: 'https://mybenefits.morganstanley.com',
          role: 'Primary Front End Developer / Content Manager',
          description: `WordPress benefits site built in 2016`,
          recent: `<a href="https://mybenefits.morganstanley.com/get-the-facts/" target="_blank">Option C page</a><br>"My Health Program" pages <a href="https://mybenefits.morganstanley.com/keyword/second-opinion-keyword/?syn=Second+Opinion&childslug=second-opinion-keyword&parentslug=my-health-programs-parent&parentname=My+Health+Programs/" target="_blank">[1]</a> <a href="https://mybenefits.morganstanley.com/keyword/castlight-keyword/?syn=Castlight&childslug=castlight-keyword&parentslug=my-health-programs-parent&parentname=My+Health+Programs/" target="_blank">[2]</a> <a href="https://mybenefits.morganstanley.com/keyword/telemedicine/?syn=Telemedicine&childslug=telemedicine&parentslug=telemedicine&parentname=Telemedicine/" target="_blank">[3]</a> <a href="https://mybenefits.morganstanley.com/keyword/lifesolutions-keyword/?syn=LifeSolutions&childslug=lifesolutions-keyword&parentslug=my-health-programs-parent&parentname=My+Health+Programs/" target="_blank">[4]</a>`
        },
        { name: 'Alliance Data', link: 'https://alliancedatagptw.com/',
          role: 'Primary Front End Developer',
          description: 'WordPress microsite built in 2018 for a "Great Places to Work" application',
          recent: 'All of it'
        },
        { name: 'Nestlé', link: 'https://healthworksatnestle.com',
          role: 'Primary Front End Developer + support dev',
          description: 'WordPress benefits site built in 2016',
          recent: 'Full redesign (team)<br><a href="http://www.healthworksatnestle.com/keyword/the-simple-7/" target="_blank">Simple 7 pages</a> (solo)'
        },
        { name: 'Discover', link: 'https://mydiscoverbenefits.com',
          role: 'Primary Front End Developer / Content Manager',
          description: 'WordPress benefits site built in 2015',
          recent: 'Home page redesign'
        },
        { name: 'DHL', link: 'https://dhlwell.com',
          role: 'Primary Front End Developer',
          description: 'WordPress benefits site built in 2016',
          recent: 'Partial branding update<br><a href="https://dhlwell.com/keyword/healthcheck/?childslug=healthcheck&syn=HealthCheck&parentslug=wellness&parentname=Wellness" target="_blank">HealthCheck page</a>'
        },
        { name: 'United Technologies', link: 'https://utchealthyyou.com',
          role: 'Primary Front End Developer',
          description: 'WordPress microsite built in 2015',
          recent: 'Full redesign<br>Bi-monthly Feature update'
        },
      ]
    }
  }
}
</script>

<style lang="scss">
@import "~/assets/scss/style.scss";

.work-samples {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  max-width: 1280px;

  @supports (display: grid) {
    display: grid;
    grid-column-gap: 1.5rem;
    grid-row-gap: 1.5rem;
    grid-template-columns: 1fr;

    @include tablet {
      grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    }
  }
}

.sample {
  border: 1px solid $dark_blue;
  padding: 1rem;

  margin: 0 .75rem 1.5rem .75rem;
  max-width: calc(100%/4 - 1.5rem);
  width: 100%;

  @supports (display: grid) {
    margin: 0;
    max-width: none;
    width: auto;
  }

  &:hover {
    border-color: $light_gold;
  }

  &-title {
    font-size: 1.25rem;
  }
  & .attributes {
    // margin-top: 1rem;
    text-align: left;
  }
  & .attribute {
    padding-top: 1rem;
  }
}

</style>
