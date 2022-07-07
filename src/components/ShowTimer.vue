<template>
  <div class = 'input-bar__buttons input-bar__timer' @click="toggleTimer">
    <span v-if="timerVissible">{{ secondsToMinutes }}:{{ milisecondsToSeconds }}</span>
  </div>
</template>

<script>
export default {
  emits: ['toggle-timer'],
  props: ['timerCounter', 'timerVissible'],
  computed: {
    secondsToMinutes(){
      return this.timerCounter === 60 ? '1' : '0'
    },
    milisecondsToSeconds(){
      return this.timerCounter === 60 ? '00' : this.timerCounter === 0 ? "00" : this.timerCounter
    }
  },
  methods: {
    toggleTimer(){
      this.$emit('toggle-timer')
    }
  }
}
</script>
