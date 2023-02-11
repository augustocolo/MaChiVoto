<template>
  <ModalView
    class="additional-analysis"
    :heading="$t('views.home.compare.additional-analysis.heading')"
    :buttons="modalButtons"
    icon="chart-bar"
    width="narrow"
    :visible="active"
    @close="close"
    @proceed="proceed"
  >
    <div v-if="currentQuestion" ref="field">
      <div v-if="currentQuestion.type === 'start'" class="additional-analysis__start">
        <p>{{ $t('views.home.compare.additional-analysis.start') }}</p>
      </div>
      <div v-else-if="currentQuestion.type === 'end'" class="additional-analysis__end">
        <p v-if="$root.$te('analysis.survey')">
          {{ $t('views.home.compare.additional-analysis.help-even-more') }}
        </p>
        <p v-else>{{ $t('views.home.compare.additional-analysis.thanks') }}</p>
      </div>
      <component
        v-else-if="currentField"
        :is="
          {
            text: 'FieldInput',
            number: 'FieldInput',
            switch: 'FieldSwitch',
            select: 'FieldSelect',
          }[currentQuestion.type]
        "
        class="additional-analysis__scroll"
        :key="currentQuestion.alias"
        :alias="currentQuestion.alias"
        :type="currentQuestion.type"
        :name="currentQuestion.name"
        :label="currentQuestion.label"
        :rules="currentQuestion.rules"
        :placeholder="
          $te(`views.home.compare.additional-analysis.fields.${currentQuestion.alias}.placeholder`)
            ? $t(
                `views.home.compare.additional-analysis.fields.${currentQuestion.alias}.placeholder`
              )
            : undefined
        "
        :description="
          $te(`views.home.compare.additional-analysis.fields.${currentQuestion.alias}.description`)
            ? $t(
                `views.home.compare.additional-analysis.fields.${currentQuestion.alias}.description`
              )
            : undefined
        "
        :options="currentQuestion.options"
        v-model:value="currentFieldValue"
      />
    </div>
  </ModalView>
</template>

<script>
export default {
  name: 'AdditionalAnalysis',
  props: {
    active: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      currentQuestionAlias: null,
    };
  },
  computed: {
    analysis() {
      return this.$store.getters['analysis/analysis'];
    },
    currentField() {
      return this.analysis.find((field) => field.name === this.currentQuestionAlias);
    },
    currentFieldValue: {
      get() {
        return this.currentField.value;
      },
      set(value) {
        this.$store.commit('analysis/setField', { name: this.currentField.name, value });
      },
    },
    currentQuestion() {
      return this.questions.find((question) => question.alias === this.currentQuestionAlias);
    },
    nextQuestion() {
      const currentIndex = this.questions.findIndex(
        (question) => question.alias === this.currentQuestionAlias
      );
      return this.questions[currentIndex + 1];
    },
    parties() {
      return this.$store.getters['parties/parties'];
    },
    questions() {
      return [
        {
          alias: 'age',
          type: 'number',
          name: this.$t('views.home.compare.additional-analysis.fields.age.name'),
          label: this.$t('views.home.compare.additional-analysis.fields.age.label'),
          rules: 'required|integer',
        },
        {
          alias: 'gender',
          type: 'switch',
          name: this.$t('views.home.compare.additional-analysis.fields.gender.name'),
          label: this.$t('views.home.compare.additional-analysis.fields.gender.label'),
          options: [
            {
              value: 'female',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.gender.options.female'
              ),
            },
            {
              value: 'male',
              option: this.$t('views.home.compare.additional-analysis.fields.gender.options.male'),
            },
            {
              value: 'other',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.gender.options.diverse'
              ),
            },
            {
              value: 'none',
              option: this.$t('views.home.compare.additional-analysis.fields.gender.options.none'),
            },
          ],
          rules: 'required',
        },
        {
          alias: 'job',
          type: 'switch',
          name: this.$t('views.home.compare.additional-analysis.fields.job.name'),
          label: this.$t('views.home.compare.additional-analysis.fields.job.label'),
          options: [
            {
              value: 'self-employed',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.self-employed'
              ),
            },
            {
              value: 'public',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.public'
              ),
            },
            {
              value: 'private',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.private'
              ),
            },
            {
              value: 'unemployed',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.unemployed'
              ),
            },
            {
              value: 'student',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.student'
              ),
            },
            {
              value: 'retired',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.retired'
              ),
            },
            {
              value: 'none',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.job.options.none'
              ),
            },
          ],
          rules: 'required',
        },
        {
          alias: 'region',
          type: 'switch',
          name: this.$t('views.home.compare.additional-analysis.fields.region.name'),
          label: this.$t('views.home.compare.additional-analysis.fields.region.label'),
          options: [
          {
              value: 'abruzzo',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.abruzzo'
              ),
            },
            {
              value: 'basilicata',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.basilicata'
              ),
            },
            {
              value: 'calabria',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.calabria'
              ),
            },
            {
              value: 'campania',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.campania'
              ),
            },
            {
              value: 'emilia-romagna',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.emilia-romagna'
              ),
            },
            {
              value: 'friuli-venezia-giulia',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.friuli-venezia-giulia'
              ),
            },
            {
              value: 'lazio',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.lazio'
              ),
            },
            {
              value: 'liguria',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.liguria'
              ),
            },
            {
              value: 'lombardia',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.lombardia'
              ),
            },
            {
              value: 'marche',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.marche'
              ),
            },
            {
              value: 'molise',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.molise'
              ),
            },
            {
              value: 'piemonte',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.piemonte'
              ),
            },
            {
              value: 'puglia',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.puglia'
              ),
            },
            {
              value: 'sardegna',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.sardegna'
              ),
            },
            {
              value: 'sicilia',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.sicilia'
              ),
            },
            {
              value: 'toscana',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.toscana'
              ),
            },
            {
              value: 'trentino-alto-adige',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.trentino-alto-adige'
              ),
            },
            {
              value: 'umbria',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.umbria'
              ),
            },
            {
              value: 'valle-aosta',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.valle-aosta'
              ),
            },
            {
              value: 'veneto',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.veneto'
              ),
            },
            {
              value: 'estero',
              option: this.$t(
                'views.home.compare.additional-analysis.fields.region.options.estero'
              ),
            }
          ],
          rules: 'required',
        },
        {
          alias: 'end',
          type: 'end',
        },
      ];
    },
    nextButtonDisabled() {
      // When mounting
      if (this.currentQuestion === undefined) {
        return true;
      }

      // Enable next button for first and last question
      if (['start', 'end'].includes(this.currentQuestion.type)) {
        return false;
      }

      // Disable next button when there is no field visible
      if (this.currentField === undefined) {
        return true;
      }

      // Disable next button when current value is null
      return this.currentField.value === null;
    },
    modalButtons() {
      // Close Button
      const buttons = [
        {
          caption: this.$t('views.home.compare.additional-analysis.buttons.close'),
          theme: 'neutral',
          eventName: 'close',
          disabled: this.currentQuestionAlias === 'start',
        },
      ];

      // Survey Button
      if (this.currentQuestionAlias === 'end' && this.$root.$te('analysis.survey')) {
        buttons.push({
          tag: 'a',
          caption: this.$t('views.home.compare.additional-analysis.buttons.open-questionnaire'),
          theme: 'primary',
          href: this.$t('analysis.survey'),
          target: '_blank',
          right: 'external-link-alt',
        });
      }

      // Start / Next Button
      if (this.currentQuestionAlias !== 'end') {
        buttons.push({
          caption:
            this.currentQuestionAlias === 'start'
              ? this.$t('views.home.compare.additional-analysis.buttons.start')
              : this.$t('views.home.compare.additional-analysis.buttons.proceed'),
          theme: 'positive',
          eventName: 'proceed',
        });
      }
      return buttons;
    },
  },
  methods: {
    close() {
      this.$store.dispatch('analysis/optOut');
    },
    proceed() {
      if (this.nextButtonDisabled) {
        return;
      }
      this.$store.dispatch('analysis/send');
      if (this.$refs.field.animate === undefined) {
        this.currentQuestionAlias = this.nextQuestion.alias || undefined;
        return;
      }
      this.$refs.field.animate([{ opacity: 1 }, { opacity: 0 }], {
        duration: 100,
      }).onfinish = () => {
        this.currentQuestionAlias = this.nextQuestion.alias || undefined;
        this.$refs.field.animate([{ opacity: 0 }, { opacity: 1 }], {
          duration: 400,
        });
      };
    },
  },
  mounted() {
    this.currentQuestionAlias = this.nextQuestion.alias;
  },
};
</script>

<style lang="scss">

div.modal__actions {
  flex-direction: column-reverse;
}
@media (min-width: 40em) {
  .additional-analysis__start,
  .additional-analysis__end {
    p {
      font-size: 1.25em;
    }
  }
}

.additional-analysis__scroll{
  overflow:scroll;
}
</style>
