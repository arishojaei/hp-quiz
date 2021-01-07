<template>
  <div class="result">
    <img
      :src="isAllCorrect ? successGif : failGif"
      alt="success gif"
    >

    <p>
      <!-- Success message -->
      <template v-if="isAllCorrect">
        <span class="playfair-font">
          Wow, you're a true wizard,
        </span>
        <small class="opa-5">
          You answered all the questions correctly
        </small>
      </template>

      <!-- Fail message -->
      <template v-else>
        <span class="playfair-font">
          Ohh miserable muggle,
        </span>
        <small class="opa-5">
          You answered {{ correctAnswers }} question correctly.
        </small>
      </template>
    </p>

    <!-- Test againg button -->
    <button @click="testAgain">
      Test again
    </button>
  </div>
</template>

<script>
import questions from '@/data/questions'
import successGif from '@/assets/images/success.gif'
import failGif from '@/assets/images/fail.gif'

export default {
  name: 'Result',
  data () {
    return {
      questions,
      correctAnswers: 0,

      successGif,
      failGif
    }
  },
  computed: {
    isAllCorrect () {
      return this.correctAnswers === this.questions.length
    }
  },
  created () {
    this.showResult()
  },
  methods: {
    /**
     * Get answers array from
     * local storage and compare
     * them with qestions array
     * to detect which answer is
     * correct
     */
    showResult () {
      const answers = JSON.parse(localStorage.getItem('answers'))
      for (const i in this.questions) {
        const isAnswerCorrect = this.questions[i].options[answers[i]].value
        if (isAnswerCorrect) {
          this.correctAnswers++
        }
      }
    },

    /**
     * Set currentStep in local storage
     * to 0 (this means first question step)
     * and then execute chechIsExamDone
     * funtion in App component
     */
    testAgain () {
      localStorage.setItem('currentStep', 0)
      this.$parent.checkIsExamDone()
    }
  }
}
</script>
