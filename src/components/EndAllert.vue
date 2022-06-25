<template>
  <h1>{{ words }} WPM</h1>
  <h3>Correct words - {{ correctWords }}</h3>
  <h3>Wrong words - {{ wrongWords }}</h3>
</template>

<script>
export default {
  props: ['words', 'correctWords', 'wrongWords'],
}
</script>