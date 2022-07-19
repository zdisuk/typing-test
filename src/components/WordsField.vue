<template>
  <div class="words-field">
    <h2 class="words-field__header">Settings</h2>
    <select class="words-field__dropdown" v-model="timerValue">
      <option value="half">30s</option>
      <option value="one">1min</option>
      <option value="two">2min</option>
      <option value="five">5min</option>
      <option value="ten">10min</option>
    </select>
    <p class="words-field__note">
      If you want to add a word, separate each word with "Space"
    </p>
    <textarea class="words-field__area" v-model="words"></textarea>
    <button class="words-field__button input-bar__buttons" @click="setWords">
      Submit
    </button>
  </div>
</template>

<script>
export default {
  props: ["words", "timerValue"],
  emits: ["submit-words"],
  methods: {
    setWords() {
      this.$emit("submit-words", this.words, this.timerValue);
    },
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
    background: rgba(35, 35, 35, 0.8235294118);
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
  &__button {
    margin: 25px 0 10px 0;
    width: 150px;
    background-color: rgba(35, 35, 35, 0.8235294118);
    color: white;
    font-size: 1em;
    &:hover {
      background-color: #2323237d;
    }
    &:focus {
      background-color: #2323237d;
    }
  }

}
</style>