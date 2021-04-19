<template>
  <div :class="$style.item">
    <div :class="$style.wrapper">
      <div :class="$style.ratingWrapper">
        <img :class="$style.star" src="../static/star.svg">
        <span :class="$style.rating">
          {{ item.rating }}
        </span>
      </div>
      <img :src="'https://frontend-test.idaproject.com' + item.photo" :class="$style.img">
      <img src="../static/cart.svg" :class="$style.cart" @click="addItemInCart(item)">
    </div>
    <p :class="$style.name">
      {{ item.name }}
    </p>
    <p :class="$style.price">
      {{ item.price }} ₽
    </p>
  </div>
</template>
<script>
export default {
  inject: ['addItemInCart'],
  props: {
    item: {
      type: Object,
      required: true
    }
  }
}
</script>
<style lang='scss' module>
.item {
  display: flex;
  width: 264px;
  height: 272px;
  flex-direction: column;
  background: $white;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  position: relative;
}

.wrapper {
  padding-top: 18px;
  display: flex;
}

.ratingWrapper {
  display: flex;
  align-self: flex-start;
  position: relative;
  padding-left: 16px;
}

.star {
  position: absolute;
  width: 13.75px;
  height: 13.14px;
}

.rating {
  position: absolute;
  font-weight: bold;
  font-size: 10px;
  line-height: 13px;
  color: $yellow;
  padding-left: 4px;
  left: 30px;
}

.img {
  width: 180px;
  height: 180px;
  margin: 0 auto;
}

.cart {
  position: absolute;
  align-self: flex-start;
  width: 12px;
  height: 13.2px;
  left: 236px;
  cursor: pointer;
  opacity: .6;
    &:hover {
    opacity: 1;
    }
}

.name {
  padding-top: 10px;
  padding-left: 16px;
  font-size: 14px;
  color: $grey-light;
}

.price {
  padding-top: 6px;
  padding-left: 16px;
  font-weight: bold;
  font-size: 14px;
  line-height: 18px;
  color: $black;
}
</style>
