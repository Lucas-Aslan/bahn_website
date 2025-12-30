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
      'Vossloh: DE 12 · DE 18 · G1206 · G1700',
      'Siemens: BR 248 Vectron Dual Mode',
      'Alstom: BR 214 · BR 203 retrofit · BR 203 Handschaltrad'
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
  },
  {
    badge: 'Prüfung',
    title: 'Gestellung Wagenprüfer bis Stufe 4',
    summary:
      'Von Stufe 1 bis 4 (ehemals Wagenmeister): Abfertigung, Rangieren und umfassende Wagenprüfungen inklusive Dokumentation.',
    points: [
      'Rangierarbeiten im Güter-, Nah- und Fernverkehr',
      'Rangierarbeiten im Gleisbau und in Häfen',
      'Rangierarbeiten in Anschlüssen & Abfertigung von Zügen',
      'Erstellen von Lauffähigkeitsuntersuchungen u. v. m.'
    ]
  },
  {
    badge: 'Kippen',
    title: 'Kippwagenberechtigte',
    summary:
      'Spezialgeschulte Mitarbeitende für das sichere Kippen auf Gleisbaustellen – immer mit Qualifikation als Rangierbegleiter.',
    points: ['Geprüft und unterwiesen für Kippvorgänge auf Ihren Baustellen']
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
      <NuxtLink to="/leistungen/transport" class="performance__cta">
        Alle Leistungen ansehen
        <span aria-hidden="true">→</span>
      </NuxtLink>
    </div>

    <div class="performance__grid">
      <article
        v-for="(block, index) in performanceBlocks"
        :key="block.title"
        class="performance-card"
        :style="{ '--card-delay': `${index * 100}ms`, '--card-index': index + 1 }"
      >
        <div class="performance-card__beam" aria-hidden="true" />
        <div class="performance-card__halo" aria-hidden="true" />
        <div class="performance-card__header">
          <div class="performance-card__eyeline">
            <span class="performance-card__index">0{{ index + 1 }}</span>
            <span class="performance-card__divider" aria-hidden="true" />
            <span class="performance-card__badge">{{ block.badge }}</span>
          </div>
          <div class="performance-card__title">
            <h3>{{ block.title }}</h3>
            <p class="performance-card__summary">{{ block.summary }}</p>
          </div>
        </div>
        <ul class="performance-card__list">
          <li
            v-for="(point, pointIndex) in block.points"
            :key="point"
            class="performance-card__item"
            :style="{ '--item-index': pointIndex }"
          >
            <span class="performance-card__icon" aria-hidden="true">✦</span>
            <span class="performance-card__item-text">{{ point }}</span>
          </li>
        </ul>
        <div class="performance-card__glow" aria-hidden="true" />
      </article>
    </div>
  </section>
</template>
