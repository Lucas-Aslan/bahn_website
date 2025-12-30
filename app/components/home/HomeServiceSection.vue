<script setup lang="ts">
type Metric = {
  value: string
  label: string
}

type Service = {
  accent: string
  title: string
  description: string
}

</script>

<template>
  <section class="section js-reveal">
    <div class="section__header">
      <div class="metrics" role="list">
        <div
          v-for="metric in metrics"
          :key="metric.label"
          class="metric"
          role="listitem"
        >
          <span class="metric__value">{{ metric.value }}</span>
          <span class="metric__label">{{ metric.label }}</span>
        </div>
      </div>
    </div>

    <div class="service-grid">
      <article
        v-for="service in services"
        :key="service.title"
        class="service-card js-reveal"
      >
        <span class="service-card__accent">{{ service.accent }}</span>
        <h3>{{ service.title }}</h3>
        <p>{{ service.description }}</p>
        <div class="service-card__glow" aria-hidden="true" />
      </article>
    </div>
  </section>
</template>
