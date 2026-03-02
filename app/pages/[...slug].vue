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
  line-height: 1.3;
}

.datenschutz-content :deep(h1 a),
.datenschutz-content :deep(h2 a),
.datenschutz-content :deep(h3 a),
.datenschutz-content :deep(h4 a),
.datenschutz-content :deep(h5 a),
.datenschutz-content :deep(h6 a) {
  color: inherit;
}

.datenschutz-content {
  max-width: 72ch;
  margin: 0 auto;
  padding: 0 0 2.5rem;
}

.datenschutz-content :deep(p),
.datenschutz-content :deep(li),
.datenschutz-content :deep(blockquote) {
  font-size: clamp(1.04rem, 0.35vw + 1rem, 1.12rem);
  line-height: 1.8;
  letter-spacing: 0.01em;
}

.datenschutz-content :deep(ul),
.datenschutz-content :deep(ol) {
  padding-left: 1.4rem;
}
</style>
