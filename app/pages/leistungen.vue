<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

type PerformanceDetail = {
  id: string
  label: string
  title: string
  intro: string
  bullets?: string[]
  subline?: string
}

const details: PerformanceDetail[] = [
{
  id: 'triebfahrzeugfuehrer',
  label: 'Lok & Traktion',
  title: 'Gestellung Triebfahrzeugführer',
  intro:
    'Wir stellen qualifizierte Triebfahrzeugführer mit den erforderlichen Berechtigungen für verschiedene Traktions- und Fahrzeugeinsätze. Eine Übersicht der verfügbaren Baureihen und Einsatzmöglichkeiten erhalten Sie gerne auf Anfrage.'
},
  {
    id: 'rangierbegleiter',
    label: 'Rangier',
    title: 'Gestellung Rangierbegleiter',
    intro:
      'Unsere Rangierbegleiter sind gleichzeitig Bremsproberechtigte, Wagenprüfer und verfügen über mehrere Jahre Erfahrung im Güter- und Fernverkehr sowie auf Gleisbaustellen.',
    subline: 'Ihre Einsatzgebiete umfassen:',
    bullets: [
      'Rangierarbeiten im Güter- und Fernverkehr',
      'Rangierarbeiten im Gleisbau',
      'Rangierarbeiten in Anschlüssen'
    ]
  },
  {
    id: 'zbv',
    label: 'ZbV',
    title: 'Gestellung ZbV und Hilfslogistik',
    intro:
      'Unsere Mitarbeiter für die Funktion der besonderen Verfügung auf Ihren Gleisbaustellen erfüllen mindestens die Qualifikationen des Rangierbegleiters.'
  },
]

let revealObserver: IntersectionObserver | null = null

onMounted(() => {
  const revealables = Array.from(document.querySelectorAll<HTMLElement>('.js-reveal'))
  revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible')
          revealObserver?.unobserve(entry.target)
        }
      })
    },
    {
      threshold: 0.18,
      rootMargin: '0px 0px -8% 0px'
    }
  )

  revealables.forEach((element, index) => {
    element.style.setProperty('--reveal-delay', `${index * 100}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="leistungen-page">
    <section class="leistungen-hero section js-reveal">
      <div class="hero__pattern" aria-hidden="true" />
      <div class="leistungen-hero__grid">
        <div class="leistungen-hero__copy">
          <p class="eyebrow">Unsere Leistungen im Überblick</p>
          <h1>Unsere Leistungen</h1>
          <p class="leistungen-hero__lead">Alle Angaben basieren exakt auf den bereitgestellten Informationen.</p>
          <div class="leistungen-hero__chips">
            <span
              v-for="detail in details"
              :key="detail.id"
              class="leistungen-hero__chip"
            >
              {{ detail.title }}
            </span>
          </div>
        </div>
        <div class="leistungen-hero__visual">
          <div class="visual__frame">
            <img
              src="/images/babylon-bahndienste-leistungen.jpg"
              alt="Güterzug im Abendlicht als Symbol für präzise Darstellung"
              class="visual__image"
              loading="lazy"
            />
            <div class="visual__badge">
              <span class="badge__icon">✦</span>
              Fokus auf Fakten
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="leistungen-stack">
      <article
        v-for="(detail, index) in details"
        :id="detail.id"
        :key="detail.id"
        class="leistung-card js-reveal"
        :style="{ '--card-delay': `${index * 120}ms` }"
      >
        <div class="leistung-card__header">
          <div class="leistung-card__meta">
            <span class="leistung-card__index">0{{ index + 1 }}</span>
            <span class="leistung-card__tag">{{ detail.label }}</span>
          </div>
          <h2>{{ detail.title }}</h2>
          <p class="leistung-card__intro">{{ detail.intro }}</p>
          <p v-if="detail.subline" class="leistung-card__subline">{{ detail.subline }}</p>
        </div>
        <ul v-if="detail.bullets" class="leistung-card__list">
          <li
            v-for="(bullet, bulletIndex) in detail.bullets"
            :key="bullet"
            class="leistung-card__item"
            :style="{ '--item-index': bulletIndex }"
          >
            <span class="leistung-card__icon">✓</span>
            <span>{{ bullet }}</span>
          </li>
        </ul>
      </article>
    </section>
  </div>
</template>

<style scoped>
.leistungen-page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  color: var(--color-ink);
}

.leistungen-hero {
  position: relative;
  overflow: hidden;
  border-radius: 28px;
  background: linear-gradient(145deg, rgba(255, 255, 255, 0.96), rgba(237, 247, 242, 0.88));
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow: 0 26px 60px rgba(0, 72, 49, 0.12);
}

.hero__pattern {
  position: absolute;
  inset: 0;
  pointer-events: none;
  background:
    radial-gradient(circle at 14% 12%, rgba(199, 117, 139, 0.18), transparent 36%),
    radial-gradient(circle at 85% 90%, rgba(0, 72, 49, 0.16), transparent 30%),
    repeating-linear-gradient(120deg, rgba(0, 72, 49, 0.04) 0 2px, transparent 2px 24px);
}

.leistungen-hero__grid {
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 280px), 1fr));
  gap: 2rem;
  align-items: center;
}

.leistungen-hero__copy h1 {
  margin: 0.2rem 0 0.45rem;
  letter-spacing: -0.02em;
  font-size: clamp(2rem, 3.2vw, 2.8rem);
  color: var(--color-forest);
}

.leistungen-hero__lead {
  margin: 0;
  color: var(--color-muted);
  max-width: 42ch;
}

.leistungen-hero__chips {
  margin-top: 1.25rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.leistungen-hero__chip {
  display: inline-flex;
  align-items: center;
  padding: 0.62rem 0.95rem;
  border-radius: 999px;
  background: rgba(0, 72, 49, 0.08);
  border: 1px solid rgba(0, 72, 49, 0.2);
  color: var(--color-forest);
  font-weight: 600;
}

.leistungen-hero__visual {
  justify-self: center;
  width: min(460px, 100%);
}

.visual__frame {
  position: relative;
  aspect-ratio: 4 / 3;
  overflow: hidden;
  border-radius: 20px;
  border: 1px solid rgba(0, 72, 49, 0.18);
  box-shadow: 0 24px 52px rgba(0, 72, 49, 0.22);
}

.visual__image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.visual__badge {
  position: absolute;
  left: 14px;
  bottom: 14px;
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.58rem 0.9rem;
  border-radius: 999px;
  background: var(--color-rose);
  color: #fff;
  font-weight: 700;
  box-shadow: 0 12px 26px rgba(199, 117, 139, 0.32);
}

.leistungen-stack {
  display: grid;
  gap: 1rem;
}

.leistung-card {
  position: relative;
  background: linear-gradient(130deg, rgba(255, 255, 255, 0.95), rgba(255, 255, 255, 0.82));
  border: 1px solid rgba(0, 72, 49, 0.12);
  border-left: 7px solid var(--color-forest);
  border-radius: 20px;
  padding: 1.25rem 1.35rem;
  box-shadow: 0 16px 34px rgba(0, 72, 49, 0.1);
  opacity: 0;
  transform: translateY(24px);
  transition: transform 0.24s ease, box-shadow 0.24s ease, border-color 0.24s ease;
}

.leistung-card:hover,
.leistung-card:focus-within {
  transform: translateY(-3px);
  border-color: rgba(199, 117, 139, 0.4);
  box-shadow: 0 18px 44px rgba(0, 72, 49, 0.16);
}

.leistungen-stack .js-reveal.is-visible {
  animation: cardEnter 0.7s ease forwards;
  animation-delay: var(--card-delay, 0ms);
}

.leistung-card__header {
  display: grid;
  gap: 0.35rem;
}

.leistung-card__meta {
  display: flex;
  align-items: center;
  gap: 0.6rem;
}

.leistung-card__index {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 44px;
  height: 28px;
  padding: 0 0.55rem;
  border-radius: 999px;
  background: rgba(184, 111, 134, 0.62);
  color: #fff;
  font-weight: 800;
}

.leistung-card__tag {
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  background: rgba(0, 72, 49, 0.09);
  color: var(--color-forest);
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-size: 0.76rem;
}

.leistung-card h2 {
  margin: 0.2rem 0 0.3rem;
  color: var(--color-forest);
  font-size: clamp(1.35rem, 2.4vw, 1.85rem);
}

.leistung-card__intro {
  margin: 0;
  line-height: 1.6;
  color: var(--color-muted);
}

.leistung-card__subline {
  margin: 0.15rem 0 0;
  color: var(--color-rose);
  font-weight: 700;
}

.leistung-card__list {
  list-style: none;
  margin: 0.9rem 0 0;
  padding: 0;
  display: grid;
  gap: 0.5rem;
}

.leistung-card__item {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.6rem;
  align-items: start;
  color: var(--color-ink);
  font-weight: 600;
  opacity: 0;
  transform: translateY(8px);
}

.leistungen-stack .js-reveal.is-visible .leistung-card__item {
  animation: itemEnter 0.52s ease forwards;
  animation-delay: calc(var(--card-delay, 0ms) + var(--item-index, 0) * 90ms + 80ms);
}

.leistung-card__icon {
  width: 22px;
  height: 22px;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: rgba(0, 72, 49, 0.12);
  color: var(--color-forest);
  font-size: 0.8rem;
  font-weight: 900;
}

.js-reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
  transition-delay: var(--reveal-delay, 0ms);
}

.js-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}

@keyframes cardEnter {
  from {
    opacity: 0;
    transform: translateY(24px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes itemEnter {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@media (max-width: 720px) {
  .leistungen-hero {
    border-radius: 22px;
  }

  .leistungen-hero__grid {
    grid-template-columns: 1fr;
  }

  .leistung-card {
    padding: 1.1rem;
  }
}
</style>
