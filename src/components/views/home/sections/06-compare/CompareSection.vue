<template>
  <div class="compare-section">
    <PageSection class="compare-section__introduction" data-section="compare">
      <h3 class="compare-section__heading">Chi siamo</h3>

      <div class="compare-section__about-us__wrapper">
        
        <div class="compare-section__about-us__column">
          <p>
            <span class="compare-section__company-heading">Will Media</span> è una community di 1,9 milioni di persone e aziende consapevoli del proprio impatto sul futuro. Uno spazio per chi desidera avere una maggiore consapevolezza del mondo che lo circonda e confrontarsi con post, video e podcast data driven
          </p>
          
          <div class="compare-section__button-wrapper">
            <a
              href="https://willmedia.it/elezioni-politiche-2022"
              target="_blank"
              class="base-button base-button--theme-primary base-button--size-large base-button--text-align-center compare-section__will-button"> 
              Scopri i contenuti di Will sulle Elezioni del 25 Settembre</a>
          </div>
        </div>
        <div class="compare-section__about-us__column">
        <p><span class="compare-section__company-heading">Democratica</span> è un progetto senza scopo di lucro, ideato e sviluppato da Pietro Valfrè, Augusto Colongo e Andrea Cognolato, in collaborazione con Social Innovation Teams, la community nonprofit per progetti e startup a impatto sociale e ambientale.</p>
        <div class="compare-section__button-wrapper">
          <a
          href="https://linktr.ee/democratica"
          target="_blank"
          class="base-button base-button--theme-primary base-button--size-large base-button--text-align-center compare-section__demo-sit-button"> 
            Scopri Democratica
          </a>
          <a
          href="https://socialinnovationteams.org/"
          target="_blank"
          class="base-button base-button--theme-primary base-button--size-large base-button--text-align-center compare-section__demo-sit-button"> 
            Scopri SIT
          </a>
        </div>
        </div>
        </div>

      <h2 class="compare-section__heading">Le posizioni dei partiti</h2>
      <p>
        Abbiamo raccolto le posizioni dei partiti all'interno dei programmi elettorali o le dichiarazioni dei principali esponenti sui temi su cui hai espresso la tua posizione, tuttavia raccomandiamo la lettura integrale dei programmi per una comprensione più completa.
      </p>
      <p></p>
      <KioskModeHint v-if="kioskMode" />
      
      
    </PageSection>
    
    <PageSection
      v-for="thesis in theses"
      :key="thesis.index"
      class="compare-section__theses"
      role="region"
      :data-section="`compare-thesis-${thesis.index}`"
      :aria-label="$t('views.home.compare.section.region-aria', { count: thesis.index + 1, total })"
      :id="`compare-thesis-${thesis.index}`"
    >
      <StatementText
        :index="thesis.index"
        :status="getStatus(thesis.index)"
        :factor="thesis.factor"
        :badge="true"
      />
      <FriendsPositions :thesis="thesis" />
      <template v-for="result in results" :key="`${thesis.index}-${result.party.index}`">
        <FullAnswer :party="result.party" :thesis="thesis" />
      </template>
    </PageSection>

    <AdditionalAnalysis :active="$store.getters['analysis/optIn'] === true" />
    <AnalysisBanner v-if="$store.getters['analysis/enabled']" />
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import AdditionalAnalysis from '/src/components/views/home/sections/06-compare/AdditionalAnalysis.vue';
import AnalysisBanner from '/src/components/views/home/sections/06-compare/AnalysisBanner.vue';
import FullAnswer from '/src/components/views/home/sections/06-compare/FullAnswer.vue';
import FriendsPositions from '/src/components/views/home/sections/06-compare/FriendsPositions.vue';
import KioskModeHint from '/src/components/views/home/sections/06-compare/KioskModeHint.vue';
import PageSection from '/src/components/elements/PageSection.vue';
import StatementText from '/src/components/views/home/sections/03-theses/StatementText.vue';

export default {
  name: 'CompareSection',
  components: {
    AdditionalAnalysis,
    AnalysisBanner,
    FullAnswer,
    FriendsPositions,
    KioskModeHint,
    PageSection,
    StatementText,
  },
  computed: {
    ...mapGetters({
      kioskMode: 'options/kioskMode',
      theses: 'theses/theses',
      total: 'theses/total',
      results: 'parties/results',
    }),
  },
  methods: {
    getStatus(index) {
      return this.$store.getters['theses/theses'][index].status;
    },
  },
};
</script>

<style lang="scss">
.compare-section__introduction {
  background-color: #fff;
  border-bottom: 2px solid var(--theme-neutral-background);
}

.compare-section__about-us__wrapper {
  background-color: #fff;
  font-size: .75rem;
  display: flex;
  flex-direction: row;
  column-gap: 1rem;
  
  @media (min-width:800px){
    font-size: 1rem;
  }
}

h3.compare-section__heading {
  margin-top: 1rem;
}

.compare-section__heading {
  color: var(--theme-primary-color);
}

.compare-section__theses + .compare-section__theses {
  border-top: 2px solid var(--theme-neutral-background);
}

.compare-section__will-button {
  margin-top: 1rem;
  font-weight: bold;
  background-color: var(--theme-primary-color)!important;
}

.compare-section__demo-sit-button {
  margin-top:1rem;
  font-weight: normal;
  background-color: #f5f5f5!important;
  font-size: 1.1em!important;
}

.compare-section__button-wrapper{
  margin-bottom: 1.5rem;
  display:flex;
  flex-direction: column;
  justify-content: space-around;
}

.compare-section__company-heading{
  color: var(--theme-primary-color);
  font-weight: bold;
}
</style>
