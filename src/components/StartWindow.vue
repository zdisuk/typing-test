<template>
  <div class="start-window">
    <button class="start-window__button" @click="startGame">Start Test</button>
  </div>
</template>

<script>
export default {
  emits: ["game-started"],
  
  methods: {
    startGame(){
      this.$emit("game-started")
    }
  }
}
</script>

<style lang="scss" scoped>
.start-window {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  &__button {
    background-color: #939393b1;
    border: none;
    color: rgb(255, 255, 255);
    font-weight: normal;
    width: 200px;
    height: 60px;
    font-size: 1.7em;
    border-radius: 4px;
    transition-duration: 0.2s;
    &:hover {
      transform: scale(1.05);
      background-color: #5b5b5be2;
      cursor: pointer;
    }
  }
}
</style>