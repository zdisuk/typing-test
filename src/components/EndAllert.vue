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
  props: ['words', 'correctWords', 'wrongWords', 'correctLetters', 'wrongLetters'],
  computed: {
    calcWPM(){
      return this.wrongWords%2===0 ?this.correctWords + (this.wrongWords/2) : this.correctWords + ((this.wrongWords/2) - 0.5)
    },
    calcLetters(){
      return this.correctLetters + this.wrongLetters
    },
    calcAccuracy(){
      if (this.wrongLetters === 0){
        return 100
      } else {
        let res = 100 - ((this.wrongLetters*100)/(this.correctLetters+this.wrongLetters))
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
  backdrop-filter: blur(3px);
  margin-top: 30px;
  font-family: sans-serif;
  border-radius: 4px;
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
      // font-family: sans-serif;
      // color: rgba(98, 255, 0, 0.592);
      color: rgba(35, 35, 35, 0.825);
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
      color: rgba(35, 35, 35, 0.825);
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