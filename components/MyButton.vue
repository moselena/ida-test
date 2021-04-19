<template>
  <button :class="$style.button" @click="$emit('handleClick')">
    <slot />
  </button>
</template>
<script>
export default {
  props: {
    handleClick: {
      type: Function,
      default: () => {}
    }
  }
}
</script>
<style lang='scss' module>
.button {
  display: block;
  width: 364px;
  height: 50px;
  background-color: $black;
  color: $white;
  border-radius: 8px;
  border-color: transparent;
  font-size: 16px;
  line-height: 21px;
  margin-top: 24px;
  cursor: pointer;
    &:active {
      background-color: $grey;
    }
    &:focus {
      outline: none;
    }
}
</style>
