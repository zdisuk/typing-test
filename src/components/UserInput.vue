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
  emits: ['space-pressed', 'key-pressed', 'backspace-pressed', 'cmd-backspace', 'shift-pressed', 'enter-pressed'],
  props: ['counter', 'letter', 'end', 'started', 'restart'],
  data(){
    return {
      enteredValue: ''
    }
  },
  methods: {
    spaceArePressed(){
      this.$emit('space-pressed', this.enteredValue)
      this.enteredValue = ''
    },
    keyPressed(e){
      if (e.key === 'Backspace'){
        this.$emit('backspace-pressed', this.enteredValue)
      } else if (e.code === 'MetaLeft'){
        this.$emit('cmd-backspace')
      } else if (e.key === 'Shift'){
        this.$emit('shift-pressed')
      } else if (e.key === 'Enter' || e.key === 'Tab'){
        this.$emit('enter-pressed')
      }
    },
    keyArePressed(e){
      this.$emit('key-pressed', e)
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
    }
  }
}
</script>