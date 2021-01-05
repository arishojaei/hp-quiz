<template>
  <div class="steps">
    <div
      class="_step"
      v-for="(q, qIndex) in questions"
      :key="qIndex"
    >
      {{ q.question }}
    </div >
  </div>
</template>

<script>
import questions from '@/data/questions'

export default {
  name: 'Steps',
  data () {
    return {
      questions
    }
  }
}
</script>
