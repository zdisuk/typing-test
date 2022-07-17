<template>
  <div class="input-bar__buttons input-bar__timer" @click="toggleTimer">
    <span v-if="timerVissible">{{ calcMinute < 10 ? '0' + calcMinute : calcMinute}}:{{ calcSecond < 10 && calcSecond !== '00' ? '0' + calcSecond : calcSecond }}</span>
  </div>
</template>

<script>
export default {
  emits: ["toggle-timer"],
  props: ["timerCounter", "timerVissible"],
  computed: {
    calcMinute() {
      return this.timerCounter === 60 || (this.timerCounter < 120 && this.timerCounter > 60)
        ? 1
        : this.timerCounter === 120 || (this.timerCounter < 180 && this.timerCounter > 120)
        ? 2
        : this.timerCounter === 180 || (this.timerCounter < 240 && this.timerCounter > 180)
        ? 3
        : this.timerCounter === 240 || (this.timerCounter < 300 && this.timerCounter > 240)
        ? 4
        : this.timerCounter === 300 || (this.timerCounter < 360 && this.timerCounter > 300)
        ? 5
        : this.timerCounter === 360 || (this.timerCounter < 420 && this.timerCounter > 360)
        ? 6
        : this.timerCounter === 420 || (this.timerCounter < 480 && this.timerCounter > 420)
        ? 7
        : this.timerCounter === 480 || (this.timerCounter < 540 && this.timerCounter > 480)
        ? 8
        : this.timerCounter === 540 || (this.timerCounter < 600 && this.timerCounter > 540)
        ? 9
        : this.timerCounter === 600
        ? 10
        : 0;
    },
    calcSecond() {
      return this.timerCounter === 60 ||
        this.timerCounter === 120 ||
        this.timerCounter === 300 ||
        this.timerCounter === 600 ||
        this.timerCounter === 0
        ? "00"
        : this.timerCounter < 60 && this.timerCounter > 0
        ? this.timerCounter
        : this.timerCounter < 120 && this.timerCounter > 60
        ? this.timerCounter - 60
        : this.timerCounter < 180 && this.timerCounter > 120
        ? this.timerCounter - 120
        : this.timerCounter < 240 && this.timerCounter > 180
        ? this.timerCounter - 180
        : this.timerCounter < 300 && this.timerCounter > 240
        ? this.timerCounter - 240
        : this.timerCounter < 360 && this.timerCounter > 300
        ? this.timerCounter - 300
        : this.timerCounter < 420 && this.timerCounter > 360
        ? this.timerCounter - 360
        : this.timerCounter < 480 && this.timerCounter > 420
        ? this.timerCounter - 420
        : this.timerCounter < 540 && this.timerCounter > 480
        ? this.timerCounter - 480
        : this.timerCounter < 600 && this.timerCounter > 540
        ? this.timerCounter - 540
        : this.timerCounter - 600
    },
  },
  methods: {
    toggleTimer() {
      this.$emit("toggle-timer");
    },
  },
};
</script>
