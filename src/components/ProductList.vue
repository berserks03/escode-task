<template>
  <div class="product-list">
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search products..."
      class="product-list__search"
    />
    <div class="product-list__grid">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @showModal="openModal"
      />
    </div>

    <Modal :isVisible="isModalVisible" @update:isVisible="isModalVisible = $event">
      <h3 class="modal__title">{{ selectedProduct.title }}</h3>
      <p class="modal__description">{{ selectedProduct.description }}</p>
    </Modal>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import ProductCard from './ProductCard.vue'
import Modal from './ModalComponent.vue'

const searchQuery = ref('')
const products = ref([])
const isModalVisible = ref(false)
const selectedProduct = ref({})

onMounted(async () => {
  const response = await fetch('https://fakestoreapi.com/products?limit=8')
  products.value = await response.json()
})

const filteredProducts = computed(() => {
  return products.value.filter((product) =>
    product.title.toLowerCase().includes(searchQuery.value.toLowerCase()),
  )
})

const openModal = (product) => {
  selectedProduct.value = product
  isModalVisible.value = true
}
</script>

<style scoped>
.product-list__search {
  width: 100%;
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.product-list__grid {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  gap: 20px;
  margin-top: 20px;
}

@media (min-width: 640px) {
  .product-list__grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .product-list__grid {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>
