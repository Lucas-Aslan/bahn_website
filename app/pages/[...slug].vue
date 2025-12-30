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
