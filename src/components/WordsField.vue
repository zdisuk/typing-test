<template>
  <div class="words-field">
    <h2 class="words-field__header">Settings</h2>
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
  props: ["words"],
  emits: ["submit-words"],
  methods: {
    setWords() {
      this.$emit("submit-words", this.words);
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
  &__note {
    padding: 15px 10px 10px 10px;
  }
  &__area {
    width: 85%;
    height: 150px;
    background-color: rgba(255, 255, 255, 0.5921568627);
    padding: 5px 10px;
    border-radius: 4px;
  }
  &__button {
    margin: 10px 0;
    background-color: #232323d2;
    color: white;
    &:hover {
      background-color: #2323237d;
    }
    &:focus{
      background-color: #2323237d;
    }
  }
}
</style>