<template>
  <header :class="$style.header">
    <p :class="$style.caption">
      TestList
    </p>
    <div :class="$style.cart" @click="handleClick">
      <img src="../static/cart.svg">
      <div :class="$style.cartCounter">
        {{ itemsInCart.length }}
      </div>
    </div>
  </header>
</template>
<script>
export default {
  props: {
    itemsInCart: {
      type: Array,
      required: true
    }
  },
  methods: {
    handleClick () {
      this.$emit('toggleCart')
    }
  }
}
</script>
<style lang='scss' module>
.header {
  background: $white;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.05);
  border-radius: 0px 0px 8px 8px;
  width: 1440px;
  height: 66px;
  display: flex;
  justify-content: space-between;
}

.caption {
  color: $grey;
  margin: 20px 0 20px 88px;
  font-family: PT Sans;
  font-weight: bold;
  font-size: 22px;
  line-height: 28px;
}

.cart {
  position: relative;
  margin: 10px 108px 20px 0;
  width: 24px;
  height: 26px;
  padding-top: 10px;
  cursor: pointer;
}

.cartCounter {
  background: $grey-light;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  position: absolute;
  top: 6px;
  left: 18px;
  font-weight: bold;
  font-size: 8px;
  line-height: 10px;
  color: $black;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
