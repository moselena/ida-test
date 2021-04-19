<template>
  <div :class="$style.wrapper">
    <div :class="$style.content">
      <img :src="'https://frontend-test.idaproject.com' + item.photo" :class="$style.img">
      <div :class="$style.info">
        <p :class="$style.name">
          {{ item.name }}
        </p>
        <p :class="$style.price">
          {{ item.price }} ₽
        </p>
        <div :class="$style.ratingWrapper">
          <img src="../static/star.svg" :class="$style.star">
          <span :class="$style.rating">
            {{ item.rating }}
          </span>
        </div>
      </div>
    </div>
    <img src="../static/remove.svg" :class="$style.remove" @click="removeItemFromCart(index)">
  </div>
</template>
<script>
export default {
  inject: ['removeItemFromCart'],
  props: {
    item: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  }
}
</script>
<style lang='scss' module>
.wrapper {
  margin-top: 16px;
  display: flex;
  justify-content: space-between;
  width: 364px;
  height: 120px;
  background: $white;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
}

.content {
  display: flex;
}

.img {
  width: 90px;
  height: 90px;
  margin: 15px;
}

.info {
  display: flex;
  flex-direction: column;
  margin-left: 34.43px -15;
  margin-top: 12px;
}

.name {
  max-width: 170px;
  font-size: 14px;
  line-height: 18px;
  color: $grey;
}

.price {
  font-weight: bold;
  font-size: 14px;
  line-height: 18px;
  color: $black;
  padding-top: 6px;
}

.ratingWrapper {
  display: flex;
  margin-top: 20px;
}

.star {
  width: 13.75px;
  height: 13.14px;
}

.rating {
  font-weight: bold;
  font-size: 10px;
  line-height: 13px;
  color: $yellow;
  padding-left: 4px;
}

.remove {
  margin-top: 49px;
  margin-right: 22px;
  width: 20px;
  height: 22px;
  cursor: pointer;
  opacity: .6;
    &:hover {
      opacity: 1;
    }
}
</style>
