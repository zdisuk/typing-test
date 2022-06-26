<template>
  <h1>{{ calcWPM }} WPM</h1>
  <h3>Correct words - {{ correctWords }}</h3>
  <h3>Wrong words - {{ wrongWords }}</h3>
</template>

<script>
export default {
  props: ['words', 'correctWords', 'wrongWords'],
  computed: {
    calcWPM(){
      return this.wrongWords%2===0 ?this.correctWords + (this.wrongWords/2) : this.correctWords + ((this.wrongWords/2) + 0.5)
    }
  }
}
</script>