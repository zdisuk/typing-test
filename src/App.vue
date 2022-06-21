<template>
  <div class="area">
    <ul class="area__words">
      <current-word></current-word>
    </ul>
  </div>
</template>

<script>
import CurrentWord from './components/CurrentWord.vue'

export default {
  components: {
    CurrentWord,
  }
}
</script>

<style lang="scss">

</style>
