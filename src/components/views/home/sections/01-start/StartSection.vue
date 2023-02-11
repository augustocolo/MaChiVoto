<template>
  <PageSection
    tag="header"
    class="start-section"
    data-section="start"
    full
    role="banner"
    :aria-roledescription="$t('views.home.start.section.banner-aria')"
  >
    <div>
      <img class="start-section__image-large" src="https://storage.googleapis.com/democratica-static-website-bucket/Machivotobanner/Ma-chi-voto-header-nobg.png"/>
      <img class="start-section__image-mobile" src="https://storage.googleapis.com/democratica-static-website-bucket/Machivotobanner/Ma-chi-voto-header-nobg-mobile.png"/>
    </div>
  </PageSection>
</template>

<script>
import OpenElectionCompassLogo from '/src/components/elements/OpenElectionCompassLogo.vue';
import PageSection from '/src/components/elements/PageSection.vue';

export default {
  name: 'StartSection',
  components: {
    OpenElectionCompassLogo,
    PageSection,
  },
};
</script>

<style lang="scss">

.start-section__image-mobile {
  display:block;
  @media screen and (min-width: 700px){
    display:none;
  }
}

.start-section__image-large {
  display:none;
  @media screen and (min-width: 700px){
    display:block;
  }
}

.start-section .page-section__container {
  padding: 0 !important;
}

.start-section {
  text-align: center;
  background-color: #F5F5F5;
}

.start-section__logo {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
}

.start-section__logo a {
  padding: 1rem
}

.start-section__logo a img {
  max-height: 50px;
  @media (min-width: 800px){
    max-height:80px;
  }
}

.start-section__heading {
  // `align-self` needed for IE11
  align-self: center;
  font-size: 3em;
  line-height: 1.25;
  text-align: center;
  max-width: 56em;
  margin: .75em auto .75em;
  @media (min-width: 38em) {
    font-size: 4em;
  }
  @media (min-width: 48em) {
    font-size: 5em;
  }
  @media (min-width: 64em) {
    font-size: 6em;
  }
}

.start-section__subtitle {
  // `align-self` needed for IE11
  align-self: center;
  font-size: 1;
  text-align: center;
  color: rgb(118, 118, 118);
  @media (min-width: 48em) {
    font-size: 1.5em;
  }
  @media (min-width: 64em) {
    font-size: 2em;
  }
}
</style>
