<template>
  <v-select
    v-model="questionData"
    :hint="question.hint"
    :label="question.label"
    :required="question.required"
    :items="question.choices"
    :error-messages="errors"
    :readonly="readOnly"
    filled
  />
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
import { Prop } from 'vue-property-decorator'
import { Question } from '@/store/form'
import { AnswerData } from '@/store/submission'

@Component
export default class Select extends Vue {
  @Prop() readonly question!: Question
  @Prop() readonly readOnly?: boolean
  @Prop() readonly errors?: Error[]

  get questionData(): AnswerData {
    return this.$store.state.submission.answers[this.question.id]
  }

  set questionData(value) {
    this.$store.commit('submission/setAnswer', {
      id: this.question.id,
      value,
    })
  }
}
</script>
