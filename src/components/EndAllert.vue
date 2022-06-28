<template>
  <h1>{{ calcWPM }} WPM</h1>
  <div>
    <h3>Correct words {{ correctWords }}</h3>
    <h3>Wrong words {{ wrongWords }}</h3>
  </div>
  <div>
    <h4>{{ correctLetters }} / {{ wrongLetters }} {{ calcLetters }}</h4>
  </div>
  <div>
    <h4>Accuracy {{ calcAccuracy }}%</h4>
  </div>
</template>

<script>
export default {
  props: ['words', 'correctWords', 'wrongWords', 'correctLetters', 'wrongLetters'],
  computed: {
    calcWPM(){
      return this.wrongWords%2===0 ?this.correctWords + (this.wrongWords/2) : this.correctWords + ((this.wrongWords/2) - 0.5)
    },
    calcLetters(){
      return this.correctLetters + this.wrongLetters
    },
    calcAccuracy(){
      function clearNumber(wletters, letters){
      let res = 100 - ((wletters*100)/letters)
      res = res.toString()
      res = [...res]
      for(let i = 0; i < res.length; i++){
        if(res[i] === '.'){
          res.splice(i+2, res.length)
          return res.join('')
        }
      }
      }
      return clearNumber(this.wrongLetters, this.calcLetters)
    }
  }
}
</script>