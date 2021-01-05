<template>
  <div class="options">
    <div
      class="_option"
      v-for="(opt, optIndex) in options"
      :key="optIndex"
    >
      <input
        type="radio"
        name="options"
        :id="`opt${optIndex}`"
        :value="optIndex"
        v-model="selectedOption"
      >
      <label :for="`opt${optIndex}`">
        {{ opt.text }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Option',
  props: {
    /**
     * List of options
     * to choose
     */
    options: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      selectedOption: ''
    }
  },
  watch: {
    selectedOption (value) {
      this.$emit('answerSelect', value)
    }
  }
}
</script>
