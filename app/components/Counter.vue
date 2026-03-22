<template>
  <div class="counter">
    <h3 class="counter__title">Counter: {{ count }}</h3>
    <button class="counter__button" @click="increment">
      Increment
    </button>
    <button class="counter__button" @click="decrement">
      Decrement
    </button>
  </div>
</template>

<script setup lang="ts">
const count = ref(0)

const increment = () => {
  count.value++
}

const decrement = () => {
  count.value--
}
</script>

<style scoped>
.counter {
  display: grid;
  gap: 0.4rem;
  width: min(100%, 360px);
}

.counter__title {
  margin: 0;
}

.counter__button {
  margin: 5px;
  background: var(--color-rose);
  color: #ffffff;
  border: 1px solid rgba(11, 122, 92, 0.4);
  border-radius: 8px;
  padding: 0.35rem 0.75rem;
  cursor: pointer;
}

@media (max-width: 480px) {
  .counter {
    width: 100%;
  }

  .counter__button {
    width: 100%;
    margin: 0;
  }
}
</style>
