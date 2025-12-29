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

<style scoped>
.metrics {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 0.8rem;
}

.metric {
  padding: 0.9rem 1rem;
  border-radius: 16px;
  background: linear-gradient(135deg, rgba(0, 255, 255, 0.12), rgba(255, 255, 255, 0.02));
  border: 1px solid rgba(255, 255, 255, 0.05);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
  display: grid;
  gap: 0.18rem;
}

.metric__value {
  font-size: 1.3rem;
  font-weight: 800;
  color: #f9d270;
}

.metric__label {
  color: #d6e6ff;
  font-size: 0.95rem;
  line-height: 1.4;
}

.service-grid {
  margin-top: 1.5rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.service-card {
  position: relative;
  overflow: hidden;
  padding: 1.4rem 1.2rem;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.05);
  min-height: 180px;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.35);
  transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
}

.service-card:hover,
.service-card:focus-within {
  transform: translateY(-4px);
  border-color: rgba(249, 210, 112, 0.4);
  box-shadow: 0 24px 60px rgba(249, 210, 112, 0.2);
}

.service-card h3 {
  margin: 0.2rem 0 0.4rem;
  font-size: 1.2rem;
}

.service-card p {
  margin: 0;
  color: #d6e6ff;
  line-height: 1.5;
  font-size: 0.98rem;
}

.service-card__accent {
  display: inline-flex;
  padding: 0.3rem 0.65rem;
  border-radius: 999px;
  background: rgba(0, 255, 255, 0.14);
  color: #74e3ff;
  font-size: 0.85rem;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.service-card__glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 80% 20%, rgba(249, 210, 112, 0.14), transparent 45%),
    radial-gradient(circle at 20% 80%, rgba(0, 255, 255, 0.12), transparent 40%);
  opacity: 0;
  transition: opacity 0.2s ease;
}

.service-card:hover .service-card__glow,
.service-card:focus-within .service-card__glow {
  opacity: 1;
}
</style>
