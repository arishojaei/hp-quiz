<template>
  <div class="result">
    <img
      :src="isAllCorrect ? successGif : failGif"
      alt="success gif"
    >

    <p>
      <template v-if="isAllCorrect">
        <span class="playfair-font">
          Wow, you're a true wizard,
        </span>
        <small class="opa-5">
          You answered all the questions correctly
        </small>
      </template>

      <template v-else>
        <span class="playfair-font">
          Ohh miserable muggle,
        </span>
        <small class="opa-5">
          You answered {{ correctAnswers }} question correctly.
        </small>
      </template>
    </p>

    <button>
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
    showResult () {
      const answers = JSON.parse(localStorage.getItem('answers'))

      for (const i in this.questions) {
        if (this.questions[i].options[answers[i]].value) {
          this.correctAnswers++
        }
      }
    }
  }
}
</script>
