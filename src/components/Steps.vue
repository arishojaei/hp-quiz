<template>
  <div class="steps">
    <div
      class="_step"
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
      </template>
    </div >
  </div>
</template>

<script>
import questions from '@/data/questions'

export default {
  name: 'Steps',
  data () {
    return {
      questions,
      currentStep: 0
    }
  }
}
</script>
