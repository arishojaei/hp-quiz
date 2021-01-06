<template>
  <div>
    <div
      v-for="(q, qIndex) in questions"
      :key="qIndex"
    >
      <template v-if="currentStep == qIndex">
        <!-- Question -->
        <h2 class="dokdo-font">
          <span class="opa-5">
            {{ qIndex+1 }}.
          </span>
          {{ q.question }}
        </h2>

        <!-- Options -->
        <app-options
          :options="q.options"
          @answerSelect="handleRecievdAnswers"
        />
      </template>
    </div >
  </div>
</template>

<script>
import questions from '@/data/questions'
import AppOptions from '@/components/Options'

export default {
  name: 'Steps',
  components: { AppOptions },
  data () {
    return {
      questions,
      answers: [],
      currentStep: 0
    }
  },
  methods: {
    /**
     * Get selected option index
     * and push it to answer array
     * until current step reached
     * to question last index
     */
    handleRecievdAnswers (payload) {
      this.answers.push(payload)
      if (this.currentStep < (this.questions.length - 1)) {
        setTimeout(() => {
          this.currentStep++
        }, 500)
      } else {
        this.$emit('finish', this.answers)
      }
    }
  }
}
</script>
