<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image" class="product-card__image" />
    <h2 class="product-card__title">{{ product.title }}</h2>
    <p class="product-card__price">{{ formatCurrency(product.price) }}</p>
    <p class="product-card__description">{{ shortenDescription(product.description) }}...</p>
    <button @click="openModal" class="product-card__more-info-button">More Info</button>
  </div>
</template>

<script setup>
const props = defineProps({
  product: Object,
})

const emit = defineEmits(['showModal'])

const openModal = () => {
  emit('showModal', props.product)
}

const formatCurrency = (value) => {
  return `$${value.toFixed(2)}`
}

const shortenDescription = (description) => {
  return description.slice(0, 60)
}
</script>

<style scoped>
.product-card {
  background-color: white;
  padding: 16px;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

.product-card:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
}

.product-card__image {
  width: 100%;
  height: 200px;
  object-fit: cover;
  border-radius: 8px;
}

.product-card__title {
  font-size: 1.25rem;
  font-weight: bold;
  margin-top: 12px;
}

.product-card__price {
  font-size: 1rem;
  color: #666;
  margin-top: 8px;
}

.product-card__description {
  font-size: 0.875rem;
  color: #888;
  margin-top: 8px;
}

.product-card__more-info-button {
  background-color: #007bff;
  color: white;
  padding: 8px 16px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  margin-top: 12px;
}

.product-card__more-info-button:hover {
  background-color: #0056b3;
}
</style>
