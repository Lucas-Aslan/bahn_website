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

<style scoped>
.performance {
  position: relative;
  background:
    radial-gradient(circle at 18% 18%, rgba(199, 117, 139, 0.12), transparent 42%),
    radial-gradient(circle at 82% 80%, rgba(0, 72, 49, 0.12), transparent 42%),
    linear-gradient(160deg, var(--color-paper), var(--color-cream));
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow:
    0 34px 90px rgba(0, 0, 0, 0.08),
    inset 0 0 0 1px rgba(255, 255, 255, 0.6);
  color: var(--color-ink);
}

.performance::before {
  content: '';
  position: absolute;
  inset: -12px;
  border-radius: 20px;
  background: radial-gradient(circle at 20% 20%, rgba(199, 117, 139, 0.12), transparent 58%),
    radial-gradient(circle at 80% 75%, rgba(0, 72, 49, 0.08), transparent 58%);
  filter: blur(18px);
  opacity: 0.35;
  z-index: 0;
  pointer-events: none;
}

.performance > * {
  position: relative;
  z-index: 1;
}

.performance__lead {
  color: var(--color-muted);
}

.performance__header {
  align-items: center;
}

.performance__cta {
  justify-self: end;
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.85rem 1.1rem;
  border-radius: 12px;
  background: linear-gradient(120deg, var(--color-rose), var(--color-forest));
  color: #ffffff;
  text-decoration: none;
  font-weight: 800;
  letter-spacing: 0.02em;
  box-shadow:
    0 18px 45px rgba(199, 117, 139, 0.2),
    inset 0 1px 0 rgba(255, 255, 255, 0.7);
  transition: transform 0.2s ease, box-shadow 0.2s ease, filter 0.2s ease;
  border: 1px solid rgba(0, 72, 49, 0.18);
}

.performance__cta:hover,
.performance__cta:focus-visible {
  transform: translateY(-2px);
  box-shadow:
    0 24px 60px rgba(0, 0, 0, 0.12),
    0 0 0 1px rgba(199, 117, 139, 0.16);
  filter: saturate(1.02);
}

.performance__grid {
  margin-top: 1.6rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.2rem;
}

.performance-card {
  position: relative;
  overflow: hidden;
  padding: 1.2rem 1.2rem 1.1rem;
  border-radius: 18px;
  background:
    radial-gradient(circle at 18% 22%, rgba(199, 117, 139, 0.08), transparent 32%),
    radial-gradient(circle at 84% 76%, rgba(0, 72, 49, 0.08), transparent 36%),
    linear-gradient(140deg, rgba(255, 255, 255, 0.96), rgba(255, 250, 243, 0.92));
  border: 1px solid rgba(0, 72, 49, 0.14);
  box-shadow:
    0 22px 55px rgba(0, 0, 0, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
  color: var(--color-ink);
  transition:
    transform 0.35s cubic-bezier(0.19, 1, 0.22, 1),
    border-color 0.3s ease,
    box-shadow 0.3s ease,
    filter 0.3s ease;
  opacity: 0;
  transform: translateY(28px) scale(0.96) rotateX(5deg);
  filter: blur(12px);
}

.performance.js-reveal.is-visible .performance-card {
  animation: performanceCardEnter 0.9s cubic-bezier(0.22, 0.85, 0.35, 1) forwards;
  animation-delay: var(--card-delay, 0ms);
}

.performance-card:hover,
.performance-card:focus-within {
  transform: translateY(-8px) scale(1.01);
  border-color: rgba(199, 117, 139, 0.35);
  box-shadow:
    0 26px 70px rgba(0, 0, 0, 0.12),
    0 0 0 1px rgba(199, 117, 139, 0.18);
  filter: saturate(1.05);
}

.performance-card__header {
  display: grid;
  gap: 0.6rem;
}

.performance-card__eyeline {
  display: flex;
  align-items: center;
  gap: 0.55rem;
  color: var(--color-muted);
  letter-spacing: 0.08em;
  font-size: 0.78rem;
  text-transform: uppercase;
}

.performance-card__index {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 42px;
  height: 26px;
  border-radius: 999px;
  border: 1px solid rgba(0, 72, 49, 0.2);
  background: rgba(199, 117, 139, 0.12);
  font-weight: 800;
  color: var(--color-forest);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.8),
    0 8px 22px rgba(0, 0, 0, 0.08);
}

.performance-card__divider {
  flex: 1;
  height: 1px;
  background: linear-gradient(90deg, rgba(199, 117, 139, 0.4), rgba(0, 72, 49, 0.35));
  filter: blur(0.25px);
  opacity: 0.7;
}

.performance-card__badge {
  width: fit-content;
  padding: 0.28rem 0.65rem;
  border-radius: 999px;
  background: rgba(0, 72, 49, 0.06);
  color: var(--color-forest);
  letter-spacing: 0.08em;
  font-size: 0.78rem;
  text-transform: uppercase;
  border: 1px solid rgba(0, 72, 49, 0.18);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.8),
    0 10px 26px rgba(0, 0, 0, 0.08);
}

.performance-card__title {
  display: grid;
  gap: 0.2rem;
}

.performance-card h3 {
  margin: 0;
  font-size: 1.24rem;
  letter-spacing: -0.01em;
  color: var(--color-ink);
}

.performance-card__summary {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.5;
  max-width: 36ch;
}

.performance-card__list {
  margin: 0.7rem 0 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.35rem;
}

.performance-card__item {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: start;
  gap: 0.55rem;
  color: var(--color-ink);
  font-weight: 700;
  opacity: 0;
  transform: translateY(8px);
  filter: blur(4px);
}

.performance-card__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: rgba(199, 117, 139, 0.12);
  border: 1px solid rgba(0, 72, 49, 0.24);
  color: var(--color-forest);
  font-size: 0.85rem;
  box-shadow:
    0 12px 26px rgba(0, 0, 0, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.85);
}

.performance-card__item-text {
  line-height: 1.45;
}

.performance-card__glow {
  position: absolute;
  inset: -12%;
  background: radial-gradient(circle at 24% 24%, rgba(199, 117, 139, 0.12), transparent 40%),
    radial-gradient(circle at 78% 70%, rgba(0, 72, 49, 0.1), transparent 42%);
  opacity: 0.35;
  pointer-events: none;
  animation: performanceGlow 6s ease-in-out infinite;
}

.performance-card__beam,
.performance-card__halo {
  position: absolute;
  pointer-events: none;
  inset: 0;
  opacity: 0.5;
  mix-blend-mode: multiply;
}

.performance-card__beam {
  background: conic-gradient(
    from 120deg,
    rgba(199, 117, 139, 0.14),
    rgba(0, 0, 0, 0),
    rgba(0, 72, 49, 0.16),
    rgba(0, 0, 0, 0)
  );
  filter: blur(22px);
  transform: rotate(calc(var(--card-index) * 2deg));
  animation: performanceBeamSpin 18s linear infinite;
}

.performance-card__halo {
  background: radial-gradient(circle at 50% 45%, rgba(199, 117, 139, 0.22), transparent 36%),
    radial-gradient(circle at 20% 80%, rgba(0, 72, 49, 0.16), transparent 34%);
  filter: blur(20px);
  animation: performanceHaloPulse 6.5s ease-in-out infinite;
  opacity: 0.4;
}

.performance-card::after {
  content: '';
  position: absolute;
  inset: 1px;
  border-radius: 17px;
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  opacity: 0.6;
  mix-blend-mode: screen;
  pointer-events: none;
  filter: blur(1px);
}

.performance-card:hover::after,
.performance-card:focus-within::after {
  opacity: 1;
}

.performance.js-reveal.is-visible .performance-card__item {
  animation: performanceItemEnter 0.7s cubic-bezier(0.22, 0.85, 0.35, 1) forwards;
  animation-delay: calc(var(--card-delay, 0ms) + var(--item-index, 0) * 90ms + 120ms);
}

@keyframes performanceCardEnter {
  0% {
    opacity: 0;
    transform: translateY(32px) scale(0.94) rotateX(6deg);
    filter: blur(14px);
  }
  60% {
    opacity: 1;
    transform: translateY(-8px) scale(1.01) rotateX(0deg);
    filter: blur(3px);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1) rotateX(0deg);
    filter: blur(0);
  }
}

@keyframes performanceItemEnter {
  0% {
    opacity: 0;
    transform: translateY(12px);
    filter: blur(6px);
  }
  60% {
    opacity: 1;
    transform: translateY(-2px);
    filter: blur(2px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes performanceGlow {
  0%,
  100% {
    opacity: 0.55;
    transform: scale(1);
  }
  50% {
    opacity: 0.92;
    transform: scale(1.04);
  }
}

@keyframes performanceBeamSpin {
  0% {
    transform: rotate(calc(var(--card-index) * 2deg)) scale(1);
  }
  100% {
    transform: rotate(calc(var(--card-index) * 2deg + 360deg)) scale(1.06);
  }
}

@keyframes performanceHaloPulse {
  0%,
  100% {
    opacity: 0.5;
    transform: scale(1);
  }
  50% {
    opacity: 0.95;
    transform: scale(1.04);
  }
}

@media (max-width: 700px) {
  .performance__header {
    grid-template-columns: 1fr;
  }

  .performance__cta {
    justify-self: start;
    width: 100%;
    justify-content: center;
  }
}
</style>
