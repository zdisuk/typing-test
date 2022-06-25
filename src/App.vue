<template>
  <div class="area">
    <ul class="area__words" v-if="wordsVisible">
      <current-word
      v-for="(item, index) in wordsInfo"
      :key="index"
      :index="index"
      :counter="counter"
      :word='item.word'
      :is-correct="item.isCorrect"
      ></current-word>
    </ul>
    <user-input :restart-game="counter" :end="end" :focus="focus" @space-pressed="specePressed" @key-pressed="keyPressed" @backspace-pressed="backspacePressed" @cmd-backspace="removeWholeWord"></user-input>
    <button @click="restartGame">Restart</button>
  </div>
  <end-allert 
  v-if="end" 
  :words="wordsCount"
  :correct-words="correctWords"
  :wrong-words="wrongWords"
  ></end-allert>
</template>

<script>
import UserInput from './components/UserInput.vue'
import CurrentWord from './components/CurrentWord.vue'
import EndAllert from './components/EndAllert.vue'

export default {
  components: {
    UserInput,
    CurrentWord,
    EndAllert,
  },
  data(){
    return {
      timerId: 0,
      focus: false,
      wordsCount: 0,
      correctWords: 0,
      wrongWords: 0,
      wordsVisible: true,
      end: false,
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
      ],
    }
  },
  watch: {
    letter(value){
      if(value === 1 && this.counter === 0){
        const that = this
        that.timerId = setTimeout(()=>{
          that.end = true
          that.wordsVisible = false
        }, 5000)
      }
    },
  },
  methods: {
    specePressed(enteredInput){
      enteredInput = enteredInput.split('')
      enteredInput.pop()
      if (enteredInput.length === 0){
        this.wordsInfo[this.counter].isCorrect = 'correct'
      } else if (enteredInput.join('') === this.wordsInfo[this.counter].word){
        this.wordsInfo[this.counter].isCorrect = 'correct'
        this.wordsCount++
        this.correctWords++
        this.counter++
      } else if (enteredInput.join('') !== this.wordsInfo[this.counter].word){
        this.wordsInfo[this.counter].isCorrect = 'wrong'
        this.wrongWords++
        this.wordsCount++
        this.counter++
      }
      this.wordsInfo[this.counter].isCorrect = 'highlight'
      this.letter = 0
    },
    keyPressed(event){
      const wordArr = this.wordsInfo[this.counter].word.split('')
      if ((event.key !== wordArr[this.letter]) && event.key !== ' '){
          this.wordsInfo[this.counter].isCorrect = 'wrong'
        } else if (event.key === wordArr[this.letter] || event.key === ' '){
          this.wordsInfo[this.counter].isCorrect = 'highlight'
        }
      this.letter++
    },
    backspacePressed(){
      if (this.letter > 0){
        this.letter--
      }
    },
    removeWholeWord(){
      this.letter = 0
    },
    restartGame(){ 
      this.wordsVisible = true
      this.end = false
      this.counter = 0
      this.letter = 0
      this.wordsCount = 0
      this.correctWords = 0
      this.wrongWords = 0
      this.focus = true
      for(let i = 0; i < this.wordsInfo.length; i++){
        this.wordsInfo[i].isCorrect = ''
        this.wordsInfo[0].isCorrect = 'highlight'
      }
      clearTimeout(this.timerId)
    },
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
