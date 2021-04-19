<template>
  <div>
    <Header :items-in-cart="itemsInCart" @toggleCart="toggleCart" />
    <div :class="$style.wrapper">
      <CatalogMenu :active-category="slug" />
      <ProductList :items="items" @mySort="mySort" />
    </div>
    <Cart v-if="isOpen" :items-in-cart="itemsInCart" @toggleCart="toggleCart" />
  </div>
</template>

<script>
import Header from '../components/Header'
import CatalogMenu from '../components/CatalogMenu'
import ProductList from '../components/ProductList'
import Cart from '../components/Cart'

export default {
  components: { Header, CatalogMenu, ProductList, Cart },
  provide () {
    return {
      addItemInCart: this.addItemInCart,
      removeItemFromCart: this.removeItemFromCart,
      removeAllItemsFromCart: this.removeAllItemsFromCart,
      toggleCart: this.toggleCart
    }
  },
  async asyncData ({ params: { slug } }) {
    const items = await fetch(`https://frontend-test.idaproject.com/api/product?category=${slug}`)
      .then(res => res.json())
    return { slug, items }
  },
  data () {
    return {
      items: [],
      itemsInCart: [],
      isOpen: false
    }
  },
  mounted () {
    this.itemsInCart = JSON.parse(localStorage.getItem('order')) || []
    this.mySort('price')
  },
  methods: {
    addItemInCart (item) {
      this.itemsInCart.push(item)
      localStorage.setItem('order', JSON.stringify(this.itemsInCart))
    },
    removeItemFromCart (index) {
      this.itemsInCart = this.itemsInCart.filter((el, ind) => ind !== index)
      localStorage.setItem('order', JSON.stringify(this.itemsInCart))
    },
    removeAllItemsFromCart () {
      this.itemsInCart = []
      localStorage.removeItem('order', JSON.stringify(this.itemsInCart))
    },
    toggleCart () {
      this.isOpen = !this.isOpen
    },
    mySort (field) {
      this.items = this.items.sort((a, b) => b[field] - a[field])
    }
  },
  fetchOnServer: true
}
</script>
<style lang='scss' module>
.wrapper {
  display: flex;
}
</style>
