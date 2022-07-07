<template>
  <button class="input-bar__buttons" @click="$emit('restart-game')">
    <slot>

    </slot>
  </button>
</template>

<script>
export default {
  emits: ['restart-game']
}
</script>