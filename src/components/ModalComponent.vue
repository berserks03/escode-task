<template>
  <div class="modal" v-if="isVisible" @click.self="closeModal">
    <div class="modal__content">
      <button class="modal__close-btn" @click="closeModal">×</button>
      <div class="modal__body">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  isVisible: {
    type: Boolean,
    required: true,
  },
})

const emit = defineEmits(['update:isVisible'])

const closeModal = () => {
  emit('update:isVisible', false)
}
</script>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
}

.modal__content {
  background-color: #ffffff;
  padding: 30px;
  border-radius: 12px;
  width: 80%;
  max-width: 600px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  position: relative;
  overflow: hidden;
}

.modal__close-btn {
  position: absolute;
  top: 15px;
  right: 15px;
  background: transparent;
  border: none;
  font-size: 2rem;
  font-weight: bold;
  color: #333;
  cursor: pointer;
  transition: color 0.2s;
}

.modal__close-btn:hover {
  color: #ff5c5c;
}

.modal__body {
  padding-top: 10px;
  font-family: 'Arial', sans-serif;
  line-height: 1.6;
}

.modal__body :deep(h3) {
  font-size: 1.5rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 15px;
}

.modal__body :deep(p) {
  font-size: 1rem;
  color: #666;
  text-align: justify;
}

.modal__body :deep(p:hover) {
  color: #222;
  transition: color 0.2s;
}
</style>
