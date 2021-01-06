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
  methods: {
    /**
     * Finish the exam
     */
    finishExam () {
      this.isExamDone = true
    }
  }
}
</script>
