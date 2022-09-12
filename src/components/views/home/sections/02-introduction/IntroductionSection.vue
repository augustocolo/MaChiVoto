<template>
  <PageSection class="introduction-section" data-section="introduction">
    <h2 class="introduction-section__heading">
      {{ $t('introduction.heading') }}
    </h2>
    <p class="introduction-section__text">
      Grazie per partecipare! **INSERIRE BREVE GUIDA**
    </p>
    <p class="introduction-section__text">
      <br>Ti ricordiamo che non abbiamo alcun tipo di collegamento con partiti o associazioni politiche, così come non è nostra intenzione procedere con una raccomandazione o indicazione rispetto alle tue volontà di voto. 
    </p>
    <p class="introduction-section__text">
      <br>Rispondendo alla prima domanda accetti che alcuni dati vengano salvati a scopo puramente di ricerca. Questi dati non potranno essere utilizzati per profilarti e/o fornirti materiale personalizzato. Puoi trovare l'informativa sulla privacy completa cliccando su questo<a href="https://www.google.com" style="color:var(--theme-primary-color)">  link</a>.
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
  background-color: #edf2f7;
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
  @media (min-width: 40em) {
    font-size: 1.25em;
  }
  @media (min-width: 64em) {
    font-size: 1.5em;
  }
}
</style>
