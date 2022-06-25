<template>
  <input type="text" v-model="enteredValue" @keyup.space="spaceArePressed" @keypress="keyArePressed">
</template>

<script>
export default {
  emits: ['space-pressed', 'key-pressed'],
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
    keyArePressed(e){
      console.log(e)
      this.$emit('key-pressed', e)
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