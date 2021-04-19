<template>
  <main :class="$style.wrapper">
    <div :class="$style.sortWrapper">
      <div :class="$style.sort">
        Сортировать по:
        <span :class="$style.sortName" @click="onSortMenu">
          {{ name }}
        </span>
        <img :class="$style.arrow" src="../static/arrow.svg">
        <div v-if="isSort" :class="$style.menu">
          <p :class="$style.menuItem" @click="onSortValue(sortPrice)">
            По цене
          </p>
          <p :class="$style.menuItem" @click="onSortValue(sortRating)">
            По популярности
          </p>
        </div>
      </div>
    </div>
    <div :class="$style.productCard">
      <ProductItem v-for="item of items" :key="item.id" :item="item" />
    </div>
  </main>
</template>
<script>
import { SORTING_MAP } from '../constants/constants'
import ProductItem from './ProductItem'
export default {
  components: { ProductItem },
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      isSort: false,
      name: ' цене ',
      sortPrice: SORTING_MAP.price,
      sortRating: SORTING_MAP.rating
    }
  },
  methods: {
    onSortMenu () {
      this.isSort = !this.isSort
    },
    onSortValue ({ name, field }) {
      this.name = name
      this.onSortMenu()
      this.$emit('mySort', field)
    }
  }
}
</script>
<style lang='scss' module>
.wrapper {
  display: flex;
  flex-direction: column;
  margin-left: 49px;
  padding-bottom: 66px;
}

.sortWrapper {
  display: flex;
  justify-content: flex-end;
}

.sort {
  position: relative;
  margin-top: 42px;
  font-size: 16px;
  line-height: 21px;
  color: $black;
}

.sortName {
  color: $grey;
  cursor: pointer;
}

.arrow {
  padding-bottom: 2px;
}

.menu {
  display: block;
  width: 160px;
  height: 68px;
  background: $white;
  box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
  position: absolute;
  z-index: 1;
  right: 0;
}

.menuItem {
  color: $black;
  cursor: pointer;
  opacity: .6;
  padding: 12px 0 0 12px;
  font-size: 14px;
  line-height: 18px;
    &:hover {
      opacity: 1;
      background: $white;
    }
}

.productCard {
  display: grid;
  grid-template-columns: repeat(4, 264px);
  grid-template-rows: 272px;
  grid-column-gap: 16px;
  grid-row-gap: 16px;
  margin-top: 34px;
}
</style>
