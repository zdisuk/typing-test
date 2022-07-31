<template>
  <div class="words-field">
    <h2 class="words-field__header">Settings</h2>
    <select class="words-field__dropdown" :value="timerValue" ref="time">
      <option value="quarter">15s</option>
      <option value="half">30s</option>
      <option value="one">1min</option>
      <option value="two">2min</option>
      <option value="five">5min</option>
      <option value="ten">10min</option>
    </select>
    <p class="words-field__note">
      If you want to add a word, separate each word with "Space"
    </p>
    <textarea class="words-field__area" :value="words" ref="textValue"></textarea>
    <div class="words-field__buttons">
      <button class="words-field__button words-field__button--submit" @click="setWords">
        Submit
      </button>
      <button class="words-field__button words-field__button--reset" @click="resetWords">
        Reset
      </button>      
    </div>
  </div>
</template>

<script>
export default {
  props: ["words", "timerValue"],
  emits: ["submit-words", "reset-words"],
  methods: {
    setWords() {
      this.$emit("submit-words", this.$refs.textValue.value, this.$refs.time.value);
    },
    resetWords(){
      fetch("https://typing-test-80715-default-rtdb.firebaseio.com/reset.json")
      .then(response => response.json())
      .then(data => {
        for (const id in data){
          this.$refs.textValue.value = data[id].words
          this.$refs.time.value = data[id].seconds
        }
      })
    }
  },
};
</script>

<style lang="scss" scoped>
.words-field {
  margin-top: 20px;
  background-color: #939393eb;
  color: #232323d2;
  width: 75%;
  border-radius: 4px;
  font-family: sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  &__header {
    background: #232323d2;
    padding: 5px 15px;
    color: white;
    font-weight: normal;
    font-size: 1em;
    width: 100%;
  }
  &__dropdown{
    margin: 10px 0;
    padding: 5px 3px;
    border-radius: 4px;
    background: #232323d2;
    color: white;
    outline: 1px solid gray;
      &:focus{
        outline: 1px solid #ffffffc8;
      }
  }
  &__note {
    padding: 10px 0 15px 0;
    font-size: 1.2em;
  }
  &__area {
    width: 87%;
    height: 150px;
    background-color: rgba(255, 255, 255, 0.5921568627);
    padding: 5px 10px;
    border-radius: 4px;
    font-size: 1em;
  }
  &__buttons {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px 0 10px 0;
  }
  &__button {
    width: 100px;
    font-size: 1em;
    margin: 0 0 0 10px;
    border-radius: 4px;
    border: none;
    outline: none;
    padding: 5px 15px;
    background: #232323d2;
    color: white;
    cursor: pointer;
    transition-duration: 0.3s;
      &:hover{
        background: #4b4b4bd2;
      }
  }

}
</style>