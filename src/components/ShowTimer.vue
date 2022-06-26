<template>
  <div class = 'timer'>
    <span class = 'timer__counter'>{{ secondsToMinutes }}:{{ milisecondsToSeconds }}</span>
  </div>
</template>

<script>
export default {
  props: ['timerCounter'],
  computed: {
    secondsToMinutes(){
      return this.timerCounter === 60 ? '1' : '0'
    },
    milisecondsToSeconds(){
      return this.timerCounter === 60 ? '00' : this.timerCounter === 0 ? "00" : this.timerCounter
    }
  }
}
</script>