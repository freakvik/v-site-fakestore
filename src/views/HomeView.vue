
<template>
  <main>
    <div class="grid gap-8 grid-cols-1 md:grid-cols-2 lg:grid-cols-4">
      <ProductCard v-for="product in products.slice(start,end)" :key="product.id" :product="product" />
    </div>
    <div class="flex justify-center pagination">
      <ul class="flex">
        <li v-if="start==10" class="mx-1 px-3 py-2 bg-gray-200 text-gray-700 hover:bg-gray-700 hover:text-gray-200 rounded-lg" @click="start -= 10, end -= 10">
          <p class="font-bold">1</p>
        </li>
        <li v-else class="mx-1 px-3 py-2 bg-gray-200 text-gray-300 rounded-lg">
          <p class="font-bald">1</p>
        </li>
        <li v-if="start==0" class="mx-1 px-3 py-2 bg-gray-200 text-gray-700 hover:bg-gray-700 hover:text-gray-200 rounded-lg" @click="start += 10, end += 10">
            <p class="font-bold">2</p>
        </li>
        <li v-else class="mx-1 px-3 py-2 bg-gray-200 text-gray-300 rounded-lg">
          <p class="font-bald">2</p>
        </li>
    </ul>
    </div>
  </main>
</template>


<script>
import { mapActions, mapState } from 'pinia'
import { useShoppingStore } from '../stores/shopping'
import ProductCard from '../components/ProductCard.vue';
export default {
  name: 'HomeView',
  data() {
    return{
      start: 0,
      end: 9
    }
  },
  components: {
    ProductCard
  },
  computed: {
    ...mapState(useShoppingStore, ['products', 'cart'])
  },
  methods: {
    truncated(data,size) {
      if (data.length > size) {
         return data.substring(0, size) + '...';
      }
      return data
    },
    ...mapActions(useShoppingStore, ['fetchProducts','addToCart', 'isInCart', 'getQuantityInCartForProduct', 'removeFromCart']),
  }
}
</script>
