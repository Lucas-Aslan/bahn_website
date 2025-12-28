<script setup lang="ts">
const route = useRoute()

const { data: page } = await useAsyncData('page-' + route.path, () => {
  return queryCollection('content').path(route.path).first()
})

const isDatenschutz = computed(() => route.path.startsWith('/datenschutz'))

if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}
</script>

<template>
  <ContentRenderer
    v-if="page"
    :class="{ 'datenschutz-content': isDatenschutz }"
    :value="page"
  />
</template>

<style scoped>
.datenschutz-content :deep(h1),
.datenschutz-content :deep(h2),
.datenschutz-content :deep(h3),
.datenschutz-content :deep(h4),
.datenschutz-content :deep(h5),
.datenschutz-content :deep(h6) {
  color: #ffffff !important;
}

.datenschutz-content :deep(h1 a),
.datenschutz-content :deep(h2 a),
.datenschutz-content :deep(h3 a),
.datenschutz-content :deep(h4 a),
.datenschutz-content :deep(h5 a),
.datenschutz-content :deep(h6 a) {
  color: inherit;
}
</style>
