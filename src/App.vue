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
    <user-input @shift-pressed="shiftPressed" :counter="counter" :letter='letter' :end="end" @space-pressed="specePressed" @key-pressed="keyPressed" @backspace-pressed="backspacePressed" @cmd-backspace="removeWholeWord"></user-input>
    <show-timer :timer-counter="timerCounter"></show-timer>
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
import ShowTimer from './components/ShowTimer.vue'

export default {
  components: {
    UserInput,
    CurrentWord,
    EndAllert,
    ShowTimer,
  },
  data(){
    return {
      wrongLetter: '',
      timerCounter: 60,
      intervalId: 0,
      timerId: 0,
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
          word: 'as',
          isCorrect: 'under',
        },
        {
          word: 'mean',
          isCorrect: '',
        },
        {
          word: 'than',
          isCorrect: '',
        },
        {
          word: 'been',
          isCorrect: '',
        },
        {
          word: 'write',
          isCorrect: '',
        },
        {
          word: 'both',
          isCorrect: '',
        },
        {
          word: 'eye',
          isCorrect: '',
        },
        {
          word: 'just',
          isCorrect: '',
        },
        {
          word: 'do',
          isCorrect: '',
        },
        {
          word: 'must',
          isCorrect: '',
        },
        {
          word: 'its',
          isCorrect: '',
        },
        {
          word: 'follow',
          isCorrect: '',
        },
        {
          word: 'man',
          isCorrect: '',
        },
        {
          word: 'his',
          isCorrect: '',
        },
        {
          word: 'that',
          isCorrect: '',
        },
        {
          word: 'know',
          isCorrect: '',
        },
        {
          word: 'put',
          isCorrect: '',
        },
        {
          word: 'use',
          isCorrect: '',
        },
        {
          word: 'would',
          isCorrect: '',
        },
        {
          word: 'open',
          isCorrect: '',
        },
        {
          word: 'my',
          isCorrect: 'highlight',
        },
        {
          word: 'between',
          isCorrect: '',
        },
        {
          word: 'we',
          isCorrect: '',
        },
        {
          word: 'say',
          isCorrect: '',
        },
        {
          word: 'might',
          isCorrect: '',
        },
        {
          word: 'name',
          isCorrect: '',
        },
        {
          word: 'sound',
          isCorrect: '',
        },
        {
          word: 'few',
          isCorrect: '',
        },
        {
          word: 'all',
          isCorrect: '',
        },
        {
          word: 'out',
          isCorrect: '',
        },
        {
          word: 'watch',
          isCorrect: '',
        },
        {
          word: 'long',
          isCorrect: '',
        },
        {
          word: 'can',
          isCorrect: '',
        },
        {
          word: 'quickly',
          isCorrect: '',
        },
        {
          word: 'thought',
          isCorrect: '',
        },
        {
          word: 'there',
          isCorrect: '',
        },
        {
          word: 'often',
          isCorrect: '',
        },
        {
          word: 'more',
          isCorrect: '',
        },
        {
          word: 'after',
          isCorrect: '',
        },
        {
          word: 'my',
          isCorrect: '',
        },
        {
          word: 'mountain',
          isCorrect: 'highlight',
        },
        {
          word: 'no',
          isCorrect: '',
        },
        {
          word: 'family',
          isCorrect: '',
        },
        {
          word: 'where',
          isCorrect: '',
        },
        {
          word: 'own',
          isCorrect: '',
        },
        {
          word: 'young',
          isCorrect: '',
        },
        {
          word: 'far',
          isCorrect: '',
        },
        {
          word: 'question',
          isCorrect: '',
        },
        {
          word: 'got',
          isCorrect: '',
        },
        {
          word: 'answer',
          isCorrect: '',
        },
        {
          word: 'this',
          isCorrect: '',
        },
        {
          word: 'time',
          isCorrect: '',
        },
        {
          word: 'side',
          isCorrect: '',
        },
        {
          word: 'group',
          isCorrect: '',
        },
        {
          word: 'too',
          isCorrect: '',
        },
        {
          word: 'for',
          isCorrect: '',
        },
        {
          word: 'mile',
          isCorrect: '',
        },
        {
          word: 'boy',
          isCorrect: '',
        },
        {
          word: 'has',
          isCorrect: '',
        },
        {
          word: 'talk',
          isCorrect: '',
        },
        {
          word: 'even',
          isCorrect: 'highlight',
        },
        {
          word: 'only',
          isCorrect: '',
        },
        {
          word: 'once',
          isCorrect: '',
        },
        {
          word: 'large',
          isCorrect: '',
        },
        {
          word: 'list',
          isCorrect: '',
        },
        {
          word: 'earth',
          isCorrect: '',
        },
        {
          word: 'such',
          isCorrect: '',
        },
        {
          word: 'move',
          isCorrect: '',
        },
        {
          word: 'tree',
          isCorrect: '',
        },
        {
          word: 'try',
          isCorrect: '',
        },
        {
          word: 'thought',
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
          word: 'as',
          isCorrect: 'under',
        },
        {
          word: 'mean',
          isCorrect: '',
        },
        {
          word: 'than',
          isCorrect: '',
        },
        {
          word: 'been',
          isCorrect: '',
        },
        {
          word: 'write',
          isCorrect: '',
        },
        {
          word: 'both',
          isCorrect: '',
        },
        {
          word: 'eye',
          isCorrect: '',
        },
        {
          word: 'just',
          isCorrect: '',
        },
        {
          word: 'do',
          isCorrect: '',
        },
        {
          word: 'must',
          isCorrect: '',
        },
        {
          word: 'its',
          isCorrect: '',
        },
        {
          word: 'follow',
          isCorrect: '',
        },
        {
          word: 'man',
          isCorrect: '',
        },
        {
          word: 'his',
          isCorrect: '',
        },
        {
          word: 'that',
          isCorrect: '',
        },
      ],
    }
  },
  watch: {
    letter(value){
      if(value === 1 && this.counter === 0){
        const that = this
        console.log('interval started')
        that.intervalId = setInterval(() => {
          this.timerCounter--
        }, 1000)
        that.timerId = setTimeout(()=>{
          that.end = true
          that.wordsVisible = false
          clearInterval(that.intervalId)
          console.log('interval stopped')
          that.timerCounter = 0
        }, 60000)
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
      this.letter = -1
    },
    keyPressed(event, enteredValue){
      const wordArr = this.wordsInfo[this.counter].word.split('')
      const inputSplit = enteredValue.split('')
      if ((inputSplit[this.letter] !== wordArr[this.letter]) && event.key !== ' ' && enteredValue !== this.wordsInfo[this.counter].word){
          this.wordsInfo[this.counter].isCorrect = 'wrong'
      } else if ((inputSplit[this.letter] === wordArr[this.letter] || event.key === ' ') && this.wordsInfo[this.counter].isCorrect !== 'wrong'){
        this.wordsInfo[this.counter].isCorrect = 'highlight'
      }
      this.letter++
    },
    backspacePressed(enteredValue){
      const wordArr = [...this.wordsInfo[this.counter].word]
      enteredValue = [...enteredValue]
        if (this.letter > 0){
          this.letter--
        }  
      if (enteredValue[this.letter-1] === wordArr[this.letter-1]){
        this.wrongLetter = wordArr[this.letter-1]
      }
      if (enteredValue[enteredValue.length-1] === this.wrongLetter || enteredValue.length === 0){
        this.wordsInfo[this.counter].isCorrect = 'highlight'
      }
    },
    removeWholeWord(){
      this.letter = 0
    },
    shiftPressed(){
      this.letter = this.letter
    },
    restartGame(){ 
      this.wordsVisible = true
      this.end = false
      this.counter = 0
      this.letter = 0
      this.wordsCount = 0
      this.correctWords = 0
      this.wrongWords = 0
      this.timerCounter = 60
      this.wrongLetter = ''

      for(let i = 0; i < this.wordsInfo.length; i++){
        this.wordsInfo[i].isCorrect = ''
        this.wordsInfo[0].isCorrect = 'highlight'
      }
      clearTimeout(this.timerId)
      clearInterval(this.intervalId)
      console.log('interval stopped')
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
