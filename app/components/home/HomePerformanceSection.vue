<script setup lang="ts">
type PerformanceBlock = {
  badge: string
  title: string
  summary: string
  points: string[]
}

const performanceBlocks: PerformanceBlock[] = [
  {
    badge: 'Lok & Traktion',
    title: 'Gestellung Triebfahrzeugführer',
    summary: 'Unsere Triebfahrzeugführer sind u. a. auf folgenden Baureihen berechtigt:',
    points: [
      'Wir stellen qualifizierte Triebfahrzeugführer mit den erforderlichen Berechtigungen für verschiedene Traktions- und Fahrzeugeinsätze. Detaillierte Informationen zu verfügbaren Baureihen und Einsatzmöglichkeiten erhalten Sie gerne auf Anfrage.'
    ]
  },
  {
    badge: 'Rangier',
    title: 'Gestellung Rangierbegleiter',
    summary:
      'Bremsproberechtigte Wagenprüfer mit langjähriger Erfahrung im Güter-, Nah- und Fernverkehr sowie auf Gleisbaustellen.',
    points: [
      'Rangierarbeiten im Güter-, Nah- und Fernverkehr',
      'Rangierarbeiten im Gleisbau',
      'Rangierarbeiten im Hafen',
      'Rangierarbeiten in Anschlüssen'
    ]
  }
]
</script>

<template>
  <section class="performance section js-reveal">
    <div class="performance__header section__header">
      <div>
        <p class="eyebrow">Leistungen</p>
        <h2>Unsere Leistungen</h2>
        <p class="section__lead performance__lead">
          Kurz und knackig zusammengefasst – die Details finden Sie auf der Leistungsseite, hier sehen Sie direkt unsere
          Kernkompetenzen.
        </p>
      </div>
      <NuxtLink to="/leistungen" class="performance__cta">Alle Leistungen ansehen →</NuxtLink>
    </div>

    <article v-for="block in performanceBlocks" :key="block.title" class="performance-card">
      <p class="performance-card__badge">{{ block.badge }}</p>
      <h3>{{ block.title }}</h3>
      <p class="performance-card__summary">{{ block.summary }}</p>
      <ul class="performance-card__list">
        <li v-for="point in block.points" :key="point">{{ point }}</li>
      </ul>
    </article>
  </section>
</template>

<style scoped>
.performance {
  display: grid;
  gap: 1.2rem;
  background: #ffffff;
}

.performance__header {
  align-items: center;
}

.performance__cta {
  justify-self: start;
  text-decoration: none;
  font-weight: 700;
  color: #ffffff;
  background: var(--color-forest);
  border-radius: 12px;
  padding: 0.75rem 1rem;
}

.performance-card {
  border: 1px solid rgba(0, 72, 49, 0.14);
  border-radius: 14px;
  padding: 1rem;
  background: rgba(0, 72, 49, 0.03);
}

.performance-card__badge {
  margin: 0 0 0.35rem;
  color: var(--color-forest);
  font-size: 0.8rem;
  font-weight: 700;
  text-transform: uppercase;
}

.performance-card h3 {
  margin: 0;
}

.performance-card__summary {
  margin: 0.45rem 0 0;
  color: var(--color-muted);
}

.performance-card__list {
  margin: 0.8rem 0 0;
  padding-left: 1.1rem;
  display: grid;
  gap: 0.35rem;
}

@media (max-width: 700px) {
  .performance__header {
    grid-template-columns: 1fr;
  }
}
</style>
