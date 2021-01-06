<template>
  <div>
    <div
      v-for="(q, qIndex) in questions"
      :key="qIndex"
    >
      <template v-if="currentStep == qIndex">
        <!-- Question -->
        <h2 class="playfair-font">
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
  watch: {
    currentStep (value) {
      localStorage.setItem('currentStep', value)
    }
  },
  created () {
    this.detectLatestStep()
  },
  methods: {
    /**
     * Add new answer to
     * answers array and
     * execute handleNextStep
     */
    handleRecievdAnswers (payload) {
      this.answers.push(payload)
      this.handleNextStep()
    },

    /**
     * Increase currentStep number
     * until currentStep reached
     * question length and execute
     * saveAnswers
     */
    handleNextStep () {
      setTimeout(() => {
        this.saveAnswers()
        this.currentStep < (this.questions.length - 1)
          ? this.currentStep++
          : this.$emit('finish')
      }, 900)
    },

    /**
     * Just set answers array
     * to local storage
     */
    saveAnswers () {
      const answers = JSON.stringify(this.answers)
      localStorage.setItem('answers', answers)
    },

    /**
     * Detect and set latest
     * step
     */
    detectLatestStep () {
      const step = localStorage.getItem('currentStep')
      this.currentStep = step | 0
    }
  }
}
</script>
