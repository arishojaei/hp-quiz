<template>
  <div class="wrapper">
    <app-result v-if="isExamDone" />
    <app-steps v-else @finish="checkAnswers" />
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
     * Get answer array and
     * set it to local storage.
     * Show result component.
     */
    checkAnswers (payload) {
      localStorage.setItem('answers', payload)
      this.isExamDone = true
    }
  }
}
</script>
