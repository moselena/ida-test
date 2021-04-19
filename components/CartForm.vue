<template>
  <div>
    <p :class="$style.text">
      Товары в корзине
    </p>
    <div>
      <CartItem v-for="(item, index) of itemsInCart" :key="index" :item="item" :index="index" />
    </div>
    <p :class="[$style.text, $style.order]">
      Оформить заказ
    </p>
    <form :class="$style.wrapper" @submit.prevent="handleSubmit">
      <input
        id="name"
        v-model="form.name"
        type="text"
        :class="$style.input"
        placeholder="Ваше имя"
        required
      >
      <input
        id="phone"
        v-model="form.phone"
        v-mask="'+7 ### ###-##-##'"
        placeholder="Телефон"
        :class="$style.input"
        type="text"
        required
      >
      <input
        id="adress"
        v-model="form.adress"
        type="text"
        :class="$style.input"
        placeholder="Адрес"
        required
      >
      <MyButton type="submit">
        Отправить
      </MyButton>
    </form>
  </div>
</template>
<script>
import CartItem from './CartItem'
import MyButton from './MyButton'

export default {
  components: { CartItem, MyButton },
  inject: ['removeAllItemsFromCart'],
  props: {
    itemsInCart: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      form: {
        name: '',
        phone: '',
        adress: ''
      }
    }
  },
  methods: {
    handleSubmit (e) {
      // const response = await fetch('#', {
      //   method: 'POST',
      //   headers: {
      //     'Content-Type': 'application/json'
      //   },
      //   body: JSON.stringify(this.form)
      // })
      // const data = await response.json()
      // console.log(data)
      const data = JSON.stringify({
        ...this.form,
        items: this.itemsInCart
      })
      console.log(data)
      this.$emit('orderIsSent')
      this.removeAllItemsFromCart()
    }
  },
  fetchOnServer: true
}
</script>
<style lang='scss' module>
.text {
  margin-top: 24px;
  font-size: 18px;
  line-height: 23px;
  color: $grey;
}

.order {
  margin-top: 24px + 8;
}

.wrapper {
  display: flex;
  flex-direction: column;
  padding-bottom: 50px;
}

.input {
  width: 364px;
  height: 50px;
  background: #F8F8F8;
  border-radius: 8px;
  border-color: transparent;
  color: $grey;
  margin-top: 16px;
  padding-left: 14px;
}

.input::placeholder {
  color: $grey-light;
  font-size: 16px;
  line-height: 21px;
}
</style>
