<template>
  <button class="input-bar__restart" @click="$emit('restart-game')">
    <slot>
      
    </slot>
  </button>
</template>

<script>
export default {
  emits: ['restart-game']
}
</script>