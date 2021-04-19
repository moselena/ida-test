<template>
  <div :class="$style.wrapper">
    <img src="../static/ok-img.svg" :class="$style.img">
    <p :class="$style.textBold">
      Заявка успешно отправлена
    </p>
    <p :class="$style.text">
      Вскоре наш менеджер свяжется с Вами
    </p>
  </div>
</template>
<script>
export default {}
</script>
<style lang='scss' module>
.wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.img {
  width: 80px;
  height: 80px;
  margin-top: calc(100vh - 366px);
}

.textBold {
  font-weight: bold;
  font-size: 24px;
  line-height: 31px;
  color: $black;
  padding-top: 24px;
}

.text {
  font-size: 16px;
  line-height: 21px;
  color: $grey;
  padding-top: 2px;
}
</style>
