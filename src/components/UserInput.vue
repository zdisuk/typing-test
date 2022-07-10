<template>
  <input type="text" 
  class="input-bar__input"
  v-model="enteredValue" 
  @keyup.space="spaceArePressed" 
  @keyup="keyPressed" 
  @keypress="keyArePressed"
  :disabled="end"
  ref="inputFocus"
  >
</template>

<script>
export default {
  emits: ['space-pressed', 'key-pressed', 'backspace-pressed', 'enter-pressed', 'clear-input'],
  props: ['counter', 'letter', 'end', 'started', 'restart'],
  data(){
    return {
      enteredValue: ''
    }
  },
  methods: {
    spaceArePressed(){
      this.$emit('space-pressed', this.enteredValue.trim())
      this.enteredValue = ''
    },
    keyPressed(e){
      if (e.key === 'Backspace'){
        this.$emit('backspace-pressed', this.enteredValue)
      } else if (e.key === 'Enter'){
        this.$emit('enter-pressed')
      }
    },
    keyArePressed(e){
      this.$emit('key-pressed', e, this.enteredValue)
    }
  },
  watch: {
    letter(v){
      if (v === 0 && this.counter === 0){
        this.enteredValue = ''
      }
    },
    end(v){
      if (v===true){
        this.enteredValue = ''
      }
    },
    started(v){
      if(v === true){
        this.$nextTick(() => this.$refs.inputFocus.focus())
      }
    },
    restart(v){
      if(v===true || v===false){
        const that = this
        setTimeout(() => {
          that.$refs.inputFocus.focus()
        }, 100)
      }
    },
    enteredValue(){
      if (this.enteredValue === ''){
        this.$emit('clear-input')
      }
    }
  }
}
</script>