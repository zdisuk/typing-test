<template>
  <li>
    <span :class="isCurrentCorrect">{{ word }}</span>
  </li>
</template>

<script>
export default {
  props: ['index', 'counter', 'word', 'isCorrect'],
  computed: {
    isCurrentCorrect(){
      if (this.index === this.counter && this.isCorrect === 'highlight'){
        return {'highlight': true}
      }
      return {'correct': this.isCorrect === 'correct', 'wrong': this.isCorrect === 'wrong'}
    }
  }
}
</script>