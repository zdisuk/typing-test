<template>
  <input type="text" 
  v-model="enteredValue" 
  @keyup.space="spaceArePressed" 
  @keyup="backspaceArePressed" 
  :disabled="end">
</template>

<script>
export default {
  emits: ['space-pressed', 'key-pressed', 'backspace-pressed', 'cmd-backspace', 'shift-pressed'],
  props: ['counter', 'letter', 'end', 'focus'],
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
    backspaceArePressed(e){
      if (e.key === 'Backspace'){
        this.$emit('backspace-pressed', this.enteredValue)
      } else if (e.code === 'MetaLeft'){
        this.$emit('cmd-backspace')
      } else if (e.key === 'Shift'){
        this.$emit('shift-pressed')
      } else {
        this.$emit('key-pressed', e, this.enteredValue) 
      }
    }
  },
  watch: {
    counter(v){
      if (v === 0 && this.letter === 0){
        this.enteredValue = ''
      }
    },
    end(v){
      if (v===true){
        this.enteredValue = ''
      }
    }
  }
}
</script>

<style scoped>
input{
  padding: 5px 10px;
  font-size: 1.3em;
  outline: none;
  width: 300px;
}
</style>