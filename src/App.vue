<template>
  <div class="wrapper">
    <app-result v-if="isExamDone" />
    <app-steps v-else @finish="finishExam" />
  </div>
</template>

<script>
export default {
  name: 'App',
  components: {
    AppSteps: () => import('@/components/Steps'),
    AppResult: () => import('@/components/Result')
  },
  data () {
    return {
      isExamDone: false
    }
  },
  created () {
    this.checkIsExamDone()
  },
  methods: {
    /**
     * Finish the exam and
     * update currentStep
     * as finish step
     */
    finishExam () {
      this.isExamDone = true
      localStorage.setItem('currentStep', -1)
    },

    /**
     * Check currentStep value
     * in local storage to decide
     * about isExamDone value
     */
    checkIsExamDone () {
      const currentStep = localStorage.getItem('currentStep')
      currentStep === '-1'
        ? this.isExamDone = true
        : this.isExamDone = false
    }
  }
}
</script>
