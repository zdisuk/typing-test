<template>
  <div class="area">
    <ul class="area__words">
      <current-word
      v-for="(item, index) in wordsInfo"
      :key="index"
      :index="index"
      :counter="counter"
      :word='item.word'
      :is-correct="item.isCorrect"
      ></current-word>
    </ul>
    <user-input @space-pressed="specePressed" @key-pressed="keyPressed"></user-input>
  </div>
</template>

<script>
import UserInput from './components/UserInput.vue'
import CurrentWord from './components/CurrentWord.vue'

export default {
  components: {
    UserInput,
    CurrentWord,
  },
  data(){
    return {
      letter: 0,
      counter: 0,
      wordsInfo: [
        {
          word: 'home',
          isCorrect: 'highlight',
        },
        {
          word: 'should',
          isCorrect: '',
        },
        {
          word: 'once',
          isCorrect: '',
        },
        {
          word: 'him',
          isCorrect: '',
        },
        {
          word: 'house',
          isCorrect: '',
        },
        {
          word: 'off',
          isCorrect: '',
        },
        {
          word: 'mountain',
          isCorrect: '',
        },
        {
          word: 'me',
          isCorrect: '',
        },
        {
          word: 'she',
          isCorrect: '',
        },
        {
          word: 'try',
          isCorrect: '',
        },
        {
          word: 'show',
          isCorrect: '',
        },
        {
          word: 'river',
          isCorrect: '',
        },
        {
          word: 'need',
          isCorrect: '',
        },
        {
          word: 'along',
          isCorrect: '',
        },
        {
          word: 'who',
          isCorrect: '',
        },
        {
          word: 'America',
          isCorrect: '',
        },
        {
          word: 'until',
          isCorrect: '',
        },
        {
          word: 'it',
          isCorrect: '',
        },
        {
          word: 'also',
          isCorrect: '',
        },
        {
          word: 'quite',
          isCorrect: '',
        },
        {
          word: 'home',
          isCorrect: 'highlight',
        },
        {
          word: 'should',
          isCorrect: '',
        },
        {
          word: 'once',
          isCorrect: '',
        },
        {
          word: 'him',
          isCorrect: '',
        },
        {
          word: 'house',
          isCorrect: '',
        },
        {
          word: 'off',
          isCorrect: '',
        },
        {
          word: 'mountain',
          isCorrect: '',
        },
        {
          word: 'me',
          isCorrect: '',
        },
        {
          word: 'she',
          isCorrect: '',
        },
        {
          word: 'try',
          isCorrect: '',
        },
        {
          word: 'show',
          isCorrect: '',
        },
        {
          word: 'river',
          isCorrect: '',
        },
        {
          word: 'need',
          isCorrect: '',
        },
        {
          word: 'along',
          isCorrect: '',
        },
        {
          word: 'who',
          isCorrect: '',
        },
        {
          word: 'America',
          isCorrect: '',
        },
        {
          word: 'until',
          isCorrect: '',
        },
        {
          word: 'it',
          isCorrect: '',
        },
        {
          word: 'also',
          isCorrect: '',
        },
        {
          word: 'quite',
          isCorrect: '',
        },
      ]
    }
  },
  methods: {
    specePressed(enteredInput){
      enteredInput = enteredInput.split('')
      enteredInput.pop()
      enteredInput = enteredInput.join('')

      if (enteredInput === this.wordsInfo[this.counter].word){
        this.wordsInfo[this.counter].isCorrect = 'correct'
        console.log(true)
      } else {
        this.wordsInfo[this.counter].isCorrect = 'wrong'
        console.log(false)
      }
      this.counter++
      this.wordsInfo[this.counter].isCorrect = 'highlight'
    },
    keyPressed(event){
      const wordArr = this.wordsInfo[this.counter].word.split('')
        if (event.key !== wordArr[this.letter]){
          this.wordsInfo[this.counter].isCorrect = 'wrong'
        } else if (event.key === wordArr[this.letter]){
          this.wordsInfo[this.counter].isCorrect = 'highlight'
        } else if (this.letter === wordArr.length-1){
          this.letter = 0
        }
        this.letter++
      console.log(wordArr[this.letter], this.letter)
    }
  }
}
</script>

<style lang="scss">
body{
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: sans-serif;
}
ul{
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 0;
  padding: 0;
}
.area{
  display: flex;
  flex-direction: column;
  align-items: center;
    &__words{
      border: 1px solid black;
      padding: 15px 30px;
      width: 400px;
      height: fit-content;
      // max-height: fit-content;
      overflow: hidden;
      margin-bottom: 30px;
    }
}
span{
  display: inline-block;
  font-size: 1.3em;
  padding: 2.5px 5px;
}
.highlight{
  background-color: #bfbfbf99;
  color: black;
}
.correct{
  color: rgb(10, 118, 10);
}
.wrong{
  background-color: rgb(218, 33, 0);
  color: white
}

</style>
