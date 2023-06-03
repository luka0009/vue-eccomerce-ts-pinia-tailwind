<template>
  <div class="card border border-blue-300 relative">
    <figure class="px-8 pt-10">
      <router-link :to="`/product/${product.id}`">
        <img
          :src="product.image"
          alt="Card Image"
          class="object-contain w-full h-64"
        />
      </router-link>
    </figure>
    <div class="card-body">
      <h2 class="card-title">
        <router-link class="link link-hover" :to="`/product/${product.id}`">{{
          product.title
        }}</router-link>
      </h2>
      <p>{{ toCurrency(product.price) }}</p>
      <div class="justify-end card-actions">
        <button
          v-if="quantity === 0"
          class="btn btn-primary absolute bottom-3 right-3"
          @click="cartStore.add(product.id)"
        >
          Add to Cart
        </button>

        <div v-else class="flex absolute bottom-3 right-3 gap-x-1">
          <button
            @click="cartStore.remove(product.id)"
            class="scale-125 px-3 py-1 text-sm font-medium text-white bg-red-600 rounded-md"
          >
            -
          </button>
          <span
            class="scale-125 px-3 py-1 text-sm font-medium text-black rounded-md"
          >
            <!-- {{ computed(() => cartStore.contents[product.id]?.quantity || 0) }} -->
            {{ quantity }}
          </span>
          <button
            @click="cartStore.add(product.id)"
            class="scale-125 px-3 py-1 text-sm font-medium text-white bg-blue-600 rounded-md"
          >
            +
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
import { useCartStore } from "../stores/cart";
import type { Product } from "../stores/products";
import { toCurrency } from "../utils/formatCurrency";

const cartStore = useCartStore();

const props = defineProps<{
  product: Product;
}>();

console.log(props.product);
const quantity = computed(
  () => cartStore.contents[props.product.id]?.quantity || 0
);
</script>
