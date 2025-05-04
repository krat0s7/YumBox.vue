<template>
  <div class="font-sans bg-white text-primary">
    <Banner />
    <main class="max-w-6xl mx-auto px-4">
      <ProductList />
      <Cart />
    </main>
  </div>
</template>

<script setup>
import Banner from './components/Banner.vue'
import ProductList from './components/ProductList.vue'
import Cart from './components/Cart.vue'
import { provide, ref } from 'vue'

const cart = ref([])

const addToCart = (product) => {
  const item = cart.value.find(p => p.id === product.id)
  item ? item.quantity++ : cart.value.push({ ...product, quantity: 1 })
}

const removeFromCart = (id) => cart.value = cart.value.filter(i => i.id !== id)
const incrementQuantity = (id) => cart.value.find(i => i.id === id).quantity++
const decrementQuantity = (id) => {
  const item = cart.value.find(i => i.id === id)
  item.quantity > 1 ? item.quantity-- : removeFromCart(id)
}

provide('cart', {
  cart,
  addToCart,
  removeFromCart,
  incrementQuantity,
  decrementQuantity
})
</script>