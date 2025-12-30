<template>
  <div>
    <h3>Counter: {{ count }}</h3>
    <button @click="increment">
      Increment
    </button>
    <button @click="decrement">
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
button {
  margin: 5px;
  background: #004831;
  color: #ffffff;
  border: 1px solid rgba(0, 72, 49, 0.4);
  border-radius: 8px;
  padding: 0.35rem 0.75rem;
  cursor: pointer;
}
</style>
