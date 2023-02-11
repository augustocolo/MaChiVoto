<template>
  <PageSection class="introduction-section" data-section="introduction">
    <h2 class="introduction-section__heading">
      {{ $t('introduction.heading') }}
    </h2>
    <p class="introduction-section__text">
      Abbiamo analizzato le proposte dei programmi elettorali in vista delle elezioni del 25 settembre per aiutarti a capire quanto le tue posizioni si sovrappongono con quelle dei principali partiti.
      <br>
    </p>
    <p class="introduction-section__text">
      Questo test vuole essere un aiuto a orientarti nella scelta, non vogliamo darti nessuna raccomandazione o indicazione rispetto alle tue volontà di voto.
    </p>
    <p class="introduction-section__text">
      Nella scelta dei partiti da includere in questo test abbiamo adottato lo stesso criterio applicato dalla legge elettorale, prendendo quindi in considerazione i programmi delle principali liste delle coalizioni (centrodestra e centrosinistra) e delle singole liste che nella Supermedia YouTrend/Agi dei sondaggi superano la soglia del 3% <a href="https://www.youtrend.it/2022/09/09/supermedia-youtrend-agi-dei-sondaggi-centrodestra-a-174-sul-centrosinistra/" style="color:var(--theme-primary-color)" target="_blank">(aggiornata al 9 settembre 2022)</a>.
    </p>
    <p class="introduction-section__text">
      Rispondendo alla prima domanda accetti che alcuni dati vengano salvati a scopo puramente di ricerca. Questi dati <b>non</b> potranno essere utilizzati per profilarti e/o fornirti materiale personalizzato. Puoi trovare l'informativa sulla privacy completa cliccando su questo<a href="https://storage.googleapis.com/democratica-static-website-bucket/Art.%2013%20GDPR_Democratica.pdf" style="color:var(--theme-primary-color)" target="_blank">  link</a>.
    </p>
  </PageSection>
</template>

<script>
import PageSection from '/src/components/elements/PageSection.vue';

export default {
  name: 'IntroductionSection',
  components: {
    PageSection,
  },
};
</script>

<style lang="scss">
.introduction-section {
  min-height: 100vh;
  display:flex;
  justify-content: center;
  flex-direction: column;
  background-color: #f5f5f5;
  color: #718096;
}

.introduction-section__heading {
  font-weight: bold;
  font-size: 1.5em;
  line-height: 1.25;
  margin-bottom: 1.5em;
  @media (min-width: 40em) {
    font-size: 1.875em;
  }
  @media (min-width: 64em) {
    font-size: 2.25em;
  }
}

.introduction-section__text {
  margin-bottom: 1em;
  @media (min-width: 40em) {
    font-size: 1.15em;
  }
  @media (min-width: 64em) {
    font-size: 1.25em;
  }
}
</style>
