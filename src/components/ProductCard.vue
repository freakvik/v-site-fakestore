<template>
   <div :class="{ 'border-green-500' : isInCart(product) }"
        class="card hover:shadow-xl w-62 bg-white transition-all"
        style="height: 400px">
      <div class="card-body ">
        <h2 class="card-title" style="height: 55px">{{ truncated(product.title, 30) }}</h2> 
        <figure><img :src="product.image" :alt="product.title" style="height: 150px"/></figure>
        <div class="flex flex-row items-center justify-between">
            <span class="font-bold text-2xl text-500">{{ product.price }}$</span>
            <label class="btn btn-link" v-bind:for="'modal-' + product.id">Details</label>
        </div>
        <div class="flex flex-row items-center">
          <h3 class="font-bold text-lg">Rating: {{ product.rating.rate }}</h3><span class="material-symbols-rounded">star</span>
        </div>
        <div class="card-actions justify-between">
          <a :class="[isInCart(product) ? '' : 'btn-secondary']" class="btn gap-2" @click="addToCart(product)">{{ isInCart(product) ? 'Add 1 more' : 'Add to cart'}} <div class="badge badge-accent">{{ getQuantityInCartForProduct(product) }}</div></a>
          <a v-if="isInCart(product)" class="btn btn-error" @click="removeFromCart(product)"><span class="material-symbols-rounded">delete</span> </a>
        </div>
      </div>
      <input type="checkbox" v-bind:id="'modal-' + product.id" class="modal-toggle" />
      <div class="modal modal-bottom sm:modal-middle">
        <div class="modal-box bg-white">
          <h3 class="font-bold text-lg">{{ product.title }}</h3>
          <p class="py-4">{{ product.description }}</p>
          <figure><img :src="product.image" :alt="product.title" style="height: 150px"/></figure>
          <p class="py-4">Category: {{ product.category }}</p>
          <h3 class="font-bold text-lg">Rating: {{ product.rating.rate }}<span class="text- material-symbols-rounded">star</span> ({{ product.rating.count }} rates)</h3>
          <div class="modal-action">
            <label v-bind:for="'modal-' + product.id" class="btn btn-ghost gap-2"><span class="material-symbols-rounded">close</span>Close</label>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import { mapActions, mapState } from 'pinia'
import { useShoppingStore } from '../stores/shopping'

export default {
  name: 'HomeView',
  props : {
    product: {
      type: Object,
      required: true
    }
  },
  computed: {
    ...mapState(useShoppingStore, ['products', 'cart'])
  },
  methods : {
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

<style>

</style>
