<template>
  <div :class="$style.overlay" @click.self="handleClose">
    <div :class="[ $style.cart, !animation ? $style.active : $style.closing ]">
      <div :class="$style.wrapper">
        <h1 :class="$style.name">
          Корзина
        </h1>
        <img src="../static/close-img.svg" :class="$style.closeImg" @click="handleClose">
      </div>
      <div v-if="isEmpty && !orderSent">
        <p :class="$style.emptyText">
          Пока что вы ничего не добавили в корзину.
        </p>
        <MyButton @handleClick="handleClose">
          Перейти к выбору
        </MyButton>
      </div>
      <div v-else>
        <CartSent v-if="orderSent" />
        <CartForm v-else :items-in-cart="itemsInCart" @orderIsSent="orderIsSent" />
      </div>
    </div>
  </div>
</template>
<script>
import CartForm from './CartForm'
import MyButton from './MyButton'
import CartSent from './CartSent'
export default {
  components: { CartForm, CartSent, MyButton },
  props: {
    itemsInCart: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      animation: false,
      orderSent: false
    }
  },
  computed: {
    isEmpty () {
      return !this.itemsInCart.length
    }
  },
  methods: {
    handleClose () {
      this.animation = !this.animation
      setTimeout(() => {
        this.$emit('toggleCart')
      }, 500)
    },
    orderIsSent () {
      this.orderSent = !this.orderSent
    }
  }
}
</script>
<style lang='scss' module>
.overlay {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 3000;
  background: rgba(255, 255, 255, .8);
}

.cart {
  width: 460px;
  height: 100vh;
  display: flex;
  flex-direction: column;
  position: fixed;
  right: 0;
  top: 0;
  padding: 0 48px;
  background: #FFFFFF;
  box-shadow: -4px 0px 16px rgba(0, 0, 0, 0.05);
  border-radius: 8px 0px 0px 8px;
  overflow: auto;
}

.cart.active {
  animation-name: appearance;
  animation-duration: .5s;
  animation-timing-function: linear;
}

@keyframes appearance {
  0% { transform: translateX(460px); }
  100% { transform: translateX(0px); }
}

.cart.closing {
  animation-name: closing;
  animation-duration: .5s;
  animation-timing-function: linear;
}

@keyframes closing {
  0% { transform: translateX(0px); }
  100% { transform: translateX(460px); }
}

.wrapper {
  display: flex;
  justify-content: space-between;
  padding-top: 52px;
}

.name {
  font-weight: bold;
  font-size: 32px;
  line-height: 41px;
  color: $black;
}

.closeImg {
  margin-right: 5px;
  margin-top: 15px;
  width: 14px;
  height: 14px;
  cursor: pointer;
}

.emptyText {
  font-size: 22px;
  line-height: 28px;
  color: $black;
  padding-top: 24px;
}
</style>
