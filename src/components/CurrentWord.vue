<template>
    <span class="words__word" :class="isCurrentCorrect">{{ word }}</span>
</template>

<script>
export default {
  props: ['index', 'counter', 'word', 'isCorrect'],
  computed: {
    isCurrentCorrect(){
      if (this.index === this.counter && this.isCorrect === 'highlight'){
        return {'highlight': true}
      }
      return {'correct': this.isCorrect === 'correct', 'wrong-letter': this.isCorrect === 'wrong-letter', 'wrong': this.isCorrect === 'wrong'}
    }
  }
}
</script>