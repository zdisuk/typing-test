<template>
  <button class="input-bar__buttons" @click="$emit('set-words')"><slot></slot></button>
</template>

<script>
export default {
  emits: ['set-words'],
}
</script>