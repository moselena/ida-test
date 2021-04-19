<template>
  <div :class="$style.wrapper">
    <div :class="$style.card">
      <h1 :class="$style.catalog">
        Каталог
      </h1>
    </div>
    <p v-if="$fetchState.pending">
      <Loader />
    </p>
    <p v-else-if="$fetchState.error">
      Ошибка
    </p>
    <div v-else :class="$style.categories">
      <ul>
        <li v-for="category of categories" :key="category.id" :class="$style.item">
          <NuxtLink :to="`/${category.id}`">
            <div :class="[$style.link, { [$style.linkActive]: isActiveCategory(category.id)}]">
              {{ category.name }}
            </div>
          </NuxtLink>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import Loader from './Loader'
export default {
  components: { Loader },
  props: {
    activeCategory: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      categories: []
    }
  },
  async fetch () {
    this.categories = await fetch('https://frontend-test.idaproject.com/api/product-category')
      .then(res => res.json())
  },
  methods: {
    isActiveCategory (id) {
      return this.activeCategory === id.toString()
    }
  },
  fetchOnServer: true
}
</script>
<style lang='scss' module>
.wrapper {
  display: flex;
  flex-direction: column;
}

.card {
  display: flex;
  justify-content: space-between;
}

.catalog {
  margin-left: 88px;
  padding-top: 32px;
  font-weight: bold;
  font-size: 32px;
  line-height: 41px;
  color: $black;
}

.categories {
  margin-left: 48px;
  margin-top: 24px;
  max-width: 160px;
}

.item{
  padding-bottom: 16px;
}

.item:last-child {
  padding-bottom: 0;
}

.link {
  font-size: 16px;
  line-height: 21px;
  color: $grey-light;
  cursor: pointer;
    &:hover {
      color: $grey;
    }
    &:active {
      color: $black;
      text-decoration: underline;
    }
}

.linkActive {
  color: $black;
  text-decoration: underline;
}
</style>
