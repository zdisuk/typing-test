<template>
  <button class="start" @click="startGame" v-if="gameStarted===false">Start Game</button>
  <div class="area" v-show="gameStarted">
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
    <input-bar>
      <user-input
      @shift-pressed="shiftPressed" 
      :counter="counter" 
      :letter='letter' 
      :end="end" 
      :started="gameStarted"
      :restart="restart"
      @space-pressed="specePressed" 
      @key-pressed="keyPressed" 
      @backspace-pressed="backspacePressed" 
      @cmd-backspace="removeWholeWord"
      @enter-pressed="enterPressed"
      ></user-input>
      <show-timer :timer-counter="timerCounter" :timer-vissible="timerVissible" @toggle-timer="toggleTimer"></show-timer>
      <button class="input-bar__restart" @click="restartGame" v-if="gameStarted"><img src="./assets/restart.png" alt="restart"></button>
    </input-bar>
  </div>
  <end-allert 
  v-if="end" 
  :words="wordsCount"
  :correct-words="correctWords"
  :wrong-words="wrongWords"
  :correct-letters="correctLetters"
  :wrong-letters="wrongLetters"
  ></end-allert>
</template>

<script>
import UserInput from './components/UserInput.vue'
import CurrentWord from './components/CurrentWord.vue'
import EndAllert from './components/EndAllert.vue'
import ShowTimer from './components/ShowTimer.vue'
import InputBar from './components/InputBar.vue'

export default {
  components: {
    UserInput,
    CurrentWord,
    EndAllert,
    ShowTimer,
    InputBar,
  },
  data(){
    return {
      timerVissible: true,
      gameStarted: false,
      restart: false,
      timerCounter: 60,
      intervalId: [],
      timerId: [],
      correctLetters: 0,
      wrongLetters: 0,
      wordsCount: 0,
      correctWords: 0,
      wrongWords: 0,
      wordsVisible: false,
      end: false,
      letter: 0,
      counter: 0,
      wordsInfo: [],
      words: "about|above|add|after|again|air|all|almost|along|also|always|America|an|and|animal|another|answer|any|are|around|as|ask|at|away|back|be|because|been|before|began|begin|being|below|between|big|book|both|boy|but|by|call|came|can|car|carry|change|children|city|close|come|could|country|cut|day|did|different|do|does|don't|down|each|earth|eat|end|enough|even|every|example|eye|face|family|far|father|feet|few|find|first|follow|food|for|form|found|four|from|get|girl|give|go|good|got|great|group|grow|had|hand|hard|has|have|he|head|hear|help|her|here|high|him|his|home|house|how|idea|if|important|in|Indian|into|is|it|its|it's|just|keep|kind|know|land|large|last|later|learn|leave|left|let|letter|life|light|like|line|list|little|live|long|look|made|make|man|many|may|me|mean|men|might|mile|miss|more|most|mother|mountain|move|much|must|my|name|near|need|never|new|next|night|no|not|now|number|of|off|often|oil|old|on|once|one|only|open|or|other|our|out|over|own|page|paper|part|people|picture|place|plant|play|point|put|question|quick|quickly|quite|read|really|right|river|run|said|same|saw|say|school|sea|second|see|seem|sentence|set|she|should|show|side|small|so|some|something|sometimes|song|soon|sound|spell|start|state|still|stop|story|study|such|take|talk|tell|than|that|the|their|them|then|there|these|they|thing|think|this|those|thought|three|through|time|to|together|too|took|tree|try|turn|two|under|until|up|us|use|very|walk|want|was|watch|water|way|we|well|went|were|what|when|where|which|while|white|who|why|will|with|without|word|work|world|would|write|year|you|young|your"
    }
  },
  watch: {
    letter(value){
      if(value === 1 && this.counter === 0){
        this.restart = false
        const that = this
        if (that.intervalId.length < 1 && that.timerId.length < 1){
          that.intervalId.push(setInterval(() => {
            that.timerCounter--
          }, 1000))
          that.timerId.push(setTimeout(()=>{
            that.end = true
            that.wordsVisible = false
            clearInterval(that.intervalId[0])
            that.timerCounter = 0
          }, 60000))
        }
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
      this.letterCount++
      const wordArr = this.wordsInfo[this.counter].word.split('')
      const inputSplit = enteredValue.split('')
      if ((inputSplit[this.letter] !== wordArr[this.letter]) && event.key !== ' ' && (event.key !== 'Enter' || event.key !== 'Tab')){
          this.wordsInfo[this.counter].isCorrect = 'wrong-letter'
          this.wrongLetters++
      } else if ((inputSplit[this.letter] === wordArr[this.letter] || event.key === ' ' || event.key === 'Enter' || event.key === 'Tab') && this.wordsInfo[this.counter].isCorrect !== 'wrong-letter'){
        this.wordsInfo[this.counter].isCorrect = 'highlight'
        this.correctLetters++
      }
      this.letter++
    },
    backspacePressed(enteredValue){
      let wordArr = [...this.wordsInfo[this.counter].word]
      let enteredValueArr = [...enteredValue]
      if (this.letter > 0){
        this.letter--
      }  
      wordArr.splice(this.letter, wordArr.length)
      enteredValueArr.splice(this.letter, 1)
      if (wordArr.join('') === enteredValueArr.join('') || enteredValue.length === 0){
        this.wordsInfo[this.counter].isCorrect = 'highlight'
      }
    },
    removeWholeWord(){
      this.letter = 0
    },
    shiftPressed(){
      this.letter = this.letter
    },
    enterPressed(){
      this.wordsInfo[this.counter].isCorrect = 'highlight'
      // clearInterval(this.intervalId[0])
      // clearTimeout(this.timerId[0])
      // this.intervalId = []
      // this.timerId = []
    },
    startGame(){
      this.gameStarted = true
      this.wordsVisible = true
      this.wordsInfo = this.randomWords(this.words)
    },
    restartGame(){ 
      this.restart = !this.restart
      this.wordsVisible = true
      this.end = false
      this.counter = 0
      this.letter = 0
      this.wordsCount = 0
      this.correctWords = 0
      this.wrongWords = 0
      this.correctLetters = 0
      this.wrongLetters = 0
      this.timerCounter = 60

      for(let i = 0; i < this.wordsInfo.length; i++){
        this.wordsInfo[i].isCorrect = ''
        this.wordsInfo[0].isCorrect = 'highlight'
      }
      clearTimeout(this.timerId[0])
      clearInterval(this.intervalId[0])
      this.timerId = []
      this.intervalId = []
      this.wordsInfo = this.randomWords(this.words)
    },
    toggleTimer(){
      this.timerVissible = !this.timerVissible
    },
    randomWords(str){
      str = [...str]
        const wordsInfo = []
        for (let i = 0; i < str.length; i++){
          if(str[i] === "|"){
            str[i] = " "
          }
        }

        str = str.join('').split(' ')

        for(let i = 0; i < 130; i++){
          wordsInfo.push({word: str[Math.floor(Math.random()*130)], isCorrect: ''})
        }

        wordsInfo[0].isCorrect = 'highlight'
        return wordsInfo
    }
  },
}
</script>

<style lang="scss">
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body{
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: 'Times New Roman, Times', serif;
  line-height: 1.6em;
  background-color: #101010;
  background-image: url('./assets/background.jpeg');
  background-repeat: no-repeat;
  background-size: 100vw;
  backdrop-filter: blur(5px);
}
#app{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
}
.start{
  background-color: #939393b1;
  border: none;
  color: rgb(255, 255, 255);
  font-weight: normal;
  width: 200px;
  height: 60px;
  // padding: 20px 40px;
  font-size: 1.7em;
  // backdrop-filter: blur(10px);
  border-radius: 4px;
  transition-duration: 0.2s;
    &:hover{
      transform: scale(1.05);
      // border-radius: 20px;
      // box-shadow: 2px 5px 3px;
      cursor: pointer;
    }
}
.area{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 800px;
    &__words{
      color: #111111;
      margin: 0;
      padding: 10px 20px;
      width: 100%;
      height: fit-content;
      overflow: hidden;
      margin-bottom: 30px;
      list-style: none;
      display: flex;
      flex-wrap: wrap;
      background-color: rgba(255, 255, 255, 0.907);
      backdrop-filter: blur(5px);
      border-radius: 4px;
    }
}
.input-bar{
    &__input{
      margin-left: 10px;
      border-radius: 4px;
      width: 500px;
      height: 100%;
      padding: 6px 12px;
      font-size: 1.8em;
      font-family: 'Times New Roman, Times', serif;
      border: none;
      outline: none;
    }
    &__timer{
      padding: 10px;
      width: 60px;
      height: 100%;
      background-color: #939393b1;
      color: white;
      font-size: 1.5em;
      margin-left: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 4px;
      cursor: pointer;
    }
    &__restart{
      width: 60px;
      height: 100%;
      margin-left: 10px;
      border-radius: 4px;
      background-color: #939393b1;
      outline: none;
      border: none;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 10px;
      cursor: pointer;
      transition-duration: 0.2s;
        &:hover{
          background-color: #93939378;
        }
        & img{
          // width: 60px;
          height: 100%;
        }
    }
}

.word{
  display: inline-block;
  font-size: 1.8em;
  padding: 5px 7px;
  border-radius: 5px;
}
.highlight{
  background-color: #acacacc3;
  // color: black;
}
.correct{
  color: green;
}
.wrong-letter{
  background-color: red;
  color: #111111
}
.wrong{
  color: red;
}

</style>
