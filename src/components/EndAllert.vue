<template>
  <div class="result">
    <header class="header"><p class="header__text">Result</p></header>
    <section class="wpm">
      <h1 class="wpm__title">{{ calcWPM }} WPM</h1>
    </section>
    <section class="lpm">
      <h4 class="lpm__title"><p class="lpm__text">Keystrokes</p><p><span class="lpm__correct-letters">{{ correctLetters }}</span> / <span class="lpm__wrong-letters">{{ wrongLetters }}</span> <span class="lpm__letters">{{ calcLetters }}</span></p></h4>
    </section>
    <section class="accuracy">
      <h4 class="accuracy__title"><p>Accuracy</p> <p>{{ calcAccuracy }}%</p></h4>
    </section>
    <section class="correct-words">
      <h4 class="correct-words__title">Correct words <p>{{ correctWords }}</p></h4>
    </section>
    <section class="wrong-words">
      <h4 class="wrong-words__title">Wrong words <p>{{ wrongWords }}</p></h4>
    </section>
  </div>
</template>

<script>
export default {
  props: ['words', 'correctWords', 'wrongWords', 'correctLetters', 'wrongLetters', 'timerSeconds'],
  computed: {
    calcWPM(){
      if (this.timerSeconds === "half"){
        if (this.wrongWords === 0){
          return this.correctWords%10 === 0 ? (this.correctWords + (this.correctWords / 10)) * 2 : (Math.round(this.correctWords + (this.correctWords/10))) * 2
        } else {
          return this.wrongWords%2===0 ? Math.round(this.correctWords + (this.wrongWords/2)) * 2 : Math.round(this.correctWords + Math.round(this.wrongWords/2)) * 2
        }
      } else if (this.timerSeconds === "one"){
        if (this.wrongWords === 0){
          return this.correctWords%10 === 0 ? this.correctWords + (this.correctWords / 10) : Math.round(this.correctWords + (this.correctWords/10))
        } else {
          return this.wrongWords%2===0 ? this.correctWords + (this.wrongWords/2) : this.correctWords + (Math.round(this.wrongWords/2))
        }
      } else if (this.timerSeconds === "two"){
        if (this.wrongWords === 0){
          return this.correctWords%10 === 0 ? (this.correctWords + (this.correctWords / 10)) / 2 : (Math.round(this.correctWords + (this.correctWords/10))) / 2
        } else {
          return this.wrongWords%2===0 ? Math.round(this.correctWords + (this.wrongWords/2)) / 2 : Math.round(this.correctWords + Math.round(this.wrongWords/2)) / 2
        }
      } else if (this.timerSeconds === "five"){
        if (this.wrongWords === 0){
          return this.correctWords%10 === 0 ? (this.correctWords + (this.correctWords / 10)) / 5 : (Math.round(this.correctWords + (this.correctWords/10))) / 5
        } else {
          return this.wrongWords%2===0 ? Math.round(this.correctWords + (this.wrongWords/2)) / 5 : Math.round(this.correctWords + Math.round(this.wrongWords/2)) / 5
        }
      } else if (this.timerSeconds === "ten"){
        if (this.wrongWords === 0){
          return this.correctWords%10 === 0 ? (this.correctWords + (this.correctWords / 10)) / 10 : (Math.round(this.correctWords + (this.correctWords/10))) / 10
        } else {
          return this.wrongWords%2===0 ? Math.round(this.correctWords + (this.wrongWords/2)) / 10 : Math.round(this.correctWords + Math.round(this.wrongWords/2)) / 10
        }
      }
    },

    calcLetters(){
      return this.correctLetters + this.wrongLetters
    },

    calcAccuracy(){
      let res = 100 - ((this.wrongLetters*100)/(this.correctLetters+this.wrongLetters))
      if (this.wrongLetters === 0){
        return 100
      } else if (this.calcLetters % 2 === 0 && res % 2 === 0){
        return res
      } else {
        res = res.toString()
        res = [...res]
        for (let i = 0; i < res.length; i++){
          if(res[i] === '.'){
            res.splice(i+2, res.length)
            return res.join('')
          } else if (res[i] === '.' && res[i+1] === 0){
            res.splice(i+1, res.length)
            return res.join('')
          }
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.result {
  color: white;
  width: 100%;
  max-width: 300px;
  background-color: #939393eb;
  margin-top: 30px;
  font-family: sans-serif;
  border-radius: 4px;
  font-size: 1em;
}
.header {
  background: rgba(35, 35, 35, 0.825);
  padding: 5px 15px;
		&__text {
      font-size: 1.2em;
		}
}
.wpm {
  padding: 25px 0;
  display: flex;
  justify-content: center;
  align-items: center;
		&__title {
      color: #232323d2;
      font-size: 2.2em;
      font-weight: bold;
		}
}
.lpm {
  background-color: #ffffff97;
  padding: 10px 20px;
  color: rgba(35, 35, 35, 0.825);
    &__title{
      display: flex;
      justify-content: space-between;
    }
		&__correct-letters {
      color: rgb(0, 140, 19);
      font-size: 1em;
		}

		&__wrong-letters {
      color: rgba(138, 2, 0, 0.66);
      font-size: 1em;
		}

		&__letters {
      font-size: 1em;
      margin-left: 10px;
		}
}
.accuracy {
    padding: 10px 20px;
		&__title {
      color: #232323d2;
      display: flex;
      justify-content: space-between;
		}
}
.correct-words {
  background-color: #ffffff97;
  color: rgba(35, 35, 35, 0.825);
  padding: 10px 20px;
    &__title{
        & p{
          color: rgb(0, 140, 19);
        }
      display: flex;
      justify-content: space-between;
    }
}
.wrong-words {
  padding: 10px 20px;
		&__title {
        & p{
          color: rgba(109, 2, 0, 0.66);
        }
      display: flex;
      justify-content: space-between;
      color: rgba(35, 35, 35, 0.825);
		}
}
</style>