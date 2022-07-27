<template>
  <button class="input-bar__buttons" @click="$emit('toggle-settings')"><slot></slot></button>
</template>

<script>
export default {
  emits: ['toggle-settings'],
}
</script>