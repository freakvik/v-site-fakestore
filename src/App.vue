<script>
import { mapActions, mapState, mapStores } from 'pinia'
import { useShoppingStore } from './stores/shopping';
export default {
  name: 'App',
  computed: {
    ...mapState(useShoppingStore, ['products', 'cart', 'cartTotal'])
  },
  mounted() {
    this.loadData()
  },
  methods: {
    ...mapActions(useShoppingStore, ['loadData']),
  }
}
</script>

<template>
  <div class="container mx-auto flex flex-col gap-4 mt-4">
    <header>
        <nav class="navbar bg-white rounded-box shadow-lg">
          <div class="flex-1 gap-4 ml-4">
            <span class="normal-case text-xl font-black">Fake Store API</span>
            <RouterLink
              v-slot="{ isActive }"
              customs
              to="/">
                <div class="btn btn-ghost" :class="[ isActive ? 'btn-active' : 'btn-ghost']" >
                  Shopping
                </div>
            </RouterLink>
          </div>
          <div class="flex-none gap-2">
            <RouterLink class="btn gap-2" to="/cart">
             Cart
             <div class="badge badge-accent badge-lg"> {{ cartTotal }}$</div>
            </RouterLink>
          </div>
        </nav>
    </header>
    <div class="flex flex-col">
      <RouterView />
    </div>

  </div>
</template>

<style>
.pagination{
  padding-bottom: 100px;
  padding-top: 30px;
}
</style>
