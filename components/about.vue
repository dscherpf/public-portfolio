<template lang="html">
  <div class="about">
    <div class="card about_dylan">
      <div class="card-image">
        Dylan Scherpf
      </div>
      <div class="card-text">Dylan is a writer-turned-devloper who took it upon himself to learn Front End web development after catching a glimpse of the field early in his career at PartnerComm, Inc.</div>
    </div>
    <div class="card about_site">
      <h2>The site</h2>
      <div>Created with <a href="https://vuejs.org/" target="_blank">Vue</a>, <a href="https://nuxtjs.org/" target="_blank">Nuxt.js</a>, and <a href="https://www.netlify.com/">Netlify</a>. NEO data from <a href="https://api.nasa.gov/api.html#neows-browse" target="_blank">NASA</a>. Animations created with <a href="http://animejs.com/" target="_blank">Anime Js</a>. <br><br>Contact through <a href="https://www.linkedin.com/in/dylan-scherpf-99499798/" target="_blank">Linkedin</a></div>
    </div>
  </div>
</template>

<script>
export default {
}
</script>

<style lang="scss">
@import "~assets/scss/style.scss";

p {
  color: $gold;
}

.card {
  text-align: left;
  margin-top: 1rem;
  max-width: 500px;
  img {
    max-width: 200px;
  }

  &-image {
    position: relative;
    background-image: url("~assets/images/dylan.jpeg");
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    text-fill-color: transparent;
    background-repeat: no-repeat;
    background-size: cover;
    height: 500px;
    text-align: center;

    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    font-size: 4rem;
    font-weight: bold;
    text-transform: uppercase;
  }
  &-image::before {
    content: '';
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    position: absolute;
    z-index: -2;
    background-image: inherit;
    background-size: cover;
  }
  &-image::after {
    content: '';
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    position: absolute;
    z-index: -1;
    background: linear-gradient(rgba(#34383e, .5) 0%, rgba(#34383e, 1) 100%);
    opacity: 1;

    transition: all 1s;
  }
  &-image:hover::after {
    opacity: .2;

    transition: all 1s;
  }

  &-text {
    margin-top: 1rem;
  }

}
</style>
