<template>
  <div class="input-bar">
    <slot>

    </slot>
  </div>
</template>

<style lang="scss" scoped>
.input-bar{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 60px;
  background: #4b4b4b6b;
  padding: 6px 20px;
  border-radius: 4px;
}
</style>