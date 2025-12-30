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
    intro: 'Unsere Triebfahrzeugführer sind u. a. auf folgenden Baureihen berechtigt:',
    bullets: ['Vossloh: DE 12 | DE 18 | G1206 | G1700', 'Siemens: BR 248 Vectron Dual Mode', 'Alstom: BR 214 | BR 203 retrofit | BR 203 Handschaltrad']
  },
  {
    id: 'rangierbegleiter',
    label: 'Rangier',
    title: 'Gestellung Rangierbegleiter',
    intro:
      'Unsere Rangierbegleiter sind gleichzeitig Bremsproberechtigte, Wagenprüfer und verfügen über mehrere Jahre Erfahrung im Güter-, Nah- und Fernverkehr sowie auf Gleisbaustellen.',
    subline: 'Ihre Einsatzgebiete umfassen:',
    bullets: [
      'Rangierarbeiten im Güter-, Nah- und Fernverkehr',
      'Rangierarbeiten im Gleisbau',
      'Rangierarbeiten im Hafen',
      'Rangierarbeiten in Anschlüssen'
    ]
  },
  {
    id: 'zbv',
    label: 'ZbV',
    title: 'Gestellung ZbV',
    intro:
      'Unsere Mitarbeiter für die Funktion der besonderen Verfügung auf Ihren Gleisbaustellen erfüllen mindestens die Qualifikationen des Rangierbegleiters.'
  },
  {
    id: 'wagenpruefer',
    label: 'Prüfung',
    title: 'Gestellung Wagenprüfer bis Stufe 4',
    intro:
      'Unsere Wagenprüfer in den Stufen 1 bis 4 (Stufe 4 = ehemals Wagenmeister) erfüllen mindestens die Qualifikationen Rangierbegleiters. Darüber hinaus sind sie mit der Stufe 3 berechtigt Züge abzufertigen sowie auch die umfassenden Tätigkeiten des Wagenprüfers Stufe 4 durchzuführen. Ihre Einsatzgebiete umfassen:',
    bullets: [
      'Rangierarbeiten im Güter- Nah- und Fernverkehr',
      'Rangierarbeiten im Gleisbau',
      'Rangierarbeiten im Hafen',
      'Rangierarbeiten in Anschlüssen',
      'Abfertigung von Zügen',
      'Erstellen von u.a. Lauffähigkeitsuntersuchungen uvm'
    ]
  },
  {
    id: 'kippwagen',
    label: 'Kipp',
    title: 'Kippwagenberechtigte',
    intro:
      'Unsere Mitarbeiter für die Funktion der Kippberechtigten auf Ihren Gleisbaustellen erfüllen mindestens die Qualifikationen des Rangierbegleiters und darüber hinaus explizit auf das Kippen geschult und durch eine Prüfungsbescheinigung berechtigt'
  }
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
      <div class="hero__bg" aria-hidden="true">
        <span class="hero__orb hero__orb--one" />
        <span class="hero__orb hero__orb--two" />
        <span class="hero__rail" />
      </div>
      <div class="leistungen-hero__grid">
        <div class="leistungen-hero__copy">
          <p class="eyebrow">Unsere Leistungen im Überblick</p>
          <h1>Leistungsseite mit maximaler Klarheit</h1>
          <p class="leistungen-hero__lead">Alle Angaben basieren exakt auf den bereitgestellten Informationen.</p>
          <div class="leistungen-hero__chips">
            <span
              v-for="detail in details"
              :key="detail.id"
              class="leistungen-hero__chip"
            >
              <span class="chip__pulse" aria-hidden="true" />
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
            <div class="visual__glow" aria-hidden="true" />
            <div class="visual__beam" aria-hidden="true" />
            <div class="visual__grid" aria-hidden="true" />
            
            <div class="visual__badge visual__badge">
              <span class="badge__icon">✦</span>
              Fokus auf Fakten
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="leistungen-stack">
      <div class="stack__rail" aria-hidden="true" />
      <article
        v-for="(detail, index) in details"
        :id="detail.id"
        :key="detail.id"
        class="leistung-card js-reveal"
        :style="{ '--card-delay': `${index * 120}ms` }"
      >
        <div class="leistung-card__halo" aria-hidden="true" />
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
            <span class="leistung-card__icon">✹</span>
            <span>{{ bullet }}</span>
          </li>
        </ul>
        <div class="leistung-card__shine" aria-hidden="true" />
      </article>
    </section>
  </div>
</template>

<style scoped>
.leistungen-page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  color: #f6f7fb;
}

.leistungen-hero {
  position: relative;
  overflow: hidden;
  background: radial-gradient(circle at 20% 30%, rgba(249, 210, 112, 0.08), transparent 32%),
    radial-gradient(circle at 80% 70%, rgba(116, 227, 255, 0.12), transparent 38%),
    linear-gradient(135deg, #040506, #0b0c12 50%, #07080b);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow:
    0 32px 80px rgba(0, 0, 0, 0.65),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
}

.hero__bg {
  position: absolute;
  inset: -20%;
  pointer-events: none;
  filter: blur(6px);
}

.hero__orb {
  position: absolute;
  width: 380px;
  height: 380px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.3), transparent 60%);
  opacity: 0.4;
  animation: float 12s ease-in-out infinite;
}

.hero__orb--one {
  top: 8%;
  left: 6%;
}

.hero__orb--two {
  bottom: 6%;
  right: 12%;
  background: radial-gradient(circle, rgba(116, 227, 255, 0.28), transparent 60%);
  animation-delay: 1.4s;
}

.hero__rail {
  position: absolute;
  left: 50%;
  top: -10%;
  width: 2px;
  height: 120%;
  background: linear-gradient(180deg, transparent, rgba(249, 210, 112, 0.5), transparent);
  transform: translateX(-50%);
  filter: drop-shadow(0 0 12px rgba(249, 210, 112, 0.6));
  animation: beamPulse 5s ease-in-out infinite;
}

.leistungen-hero__grid {
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  align-items: center;
}

.leistungen-hero__copy h1 {
  margin: 0.2rem 0 0.4rem;
  letter-spacing: -0.01em;
  font-size: clamp(1.9rem, 3vw, 2.6rem);
}

.leistungen-hero__lead {
  margin: 0;
  color: #c5cbe0;
}

.leistungen-hero__chips {
  margin-top: 1.2rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.65rem;
}

.leistungen-hero__chip {
  position: relative;
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.75rem 1rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.3);
  box-shadow:
    0 16px 40px rgba(0, 0, 0, 0.35),
    inset 0 1px 0 rgba(255, 255, 255, 0.15);
  overflow: hidden;
}

.chip__pulse {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: linear-gradient(120deg, #f9d270, #74e3ff);
  box-shadow: 0 0 16px rgba(249, 210, 112, 0.65);
  animation: pulse 1.8s ease-in-out infinite;
}

.leistungen-hero__visual {
  position: relative;
  justify-self: center;
  width: min(440px, 100%);
}

.visual__frame {
  position: relative;
  aspect-ratio: 4 / 3;
  border-radius: 18px;
  border: 1px solid rgba(255, 255, 255, 0.08);
  background: radial-gradient(circle at 25% 30%, rgba(249, 210, 112, 0.2), transparent 42%),
    radial-gradient(circle at 80% 70%, rgba(116, 227, 255, 0.2), transparent 40%),
    linear-gradient(140deg, rgba(14, 14, 20, 0.8), rgba(5, 5, 8, 0.9));
  overflow: hidden;
  box-shadow:
    0 28px 70px rgba(0, 0, 0, 0.6),
    inset 0 1px 0 rgba(255, 255, 255, 0.1);
}

.visual__glow,
.visual__beam,
.visual__grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.visual__image {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 16px;
  filter: saturate(1.05);
}

.visual__glow {
  background: conic-gradient(
    from 120deg,
    rgba(249, 210, 112, 0.18),
    rgba(116, 227, 255, 0.18),
    rgba(249, 210, 112, 0.18)
  );
  mix-blend-mode: screen;
  filter: blur(26px);
  opacity: 0.5;
  animation: spin 18s linear infinite;
}

.visual__beam {
  background: radial-gradient(circle at 50% 20%, rgba(255, 255, 255, 0.12), transparent 32%),
    radial-gradient(circle at 40% 60%, rgba(255, 255, 255, 0.08), transparent 32%);
  opacity: 0.7;
  animation: float 10s ease-in-out infinite;
}

.visual__grid {
  background: linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 36px 36px;
  opacity: 0.2;
  transform: translateY(6px);
}

.visual__badge {
  position: absolute;
  left: 12px;
  bottom: 14px;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.6rem 0.9rem;
  border-radius: 999px;
  background: rgba(6, 12, 20, 0.75);
  border: 1px solid rgba(249, 210, 112, 0.32);
  color: #f6f7fb;
  font-weight: 700;
  box-shadow:
    0 12px 28px rgba(0, 0, 0, 0.35),
    inset 0 1px 0 rgba(255, 255, 255, 0.12);
}

.visual__badge--right {
  left: auto;
  right: 12px;
  bottom: auto;
  top: 14px;
  border-color: rgba(116, 227, 255, 0.42);
}

.badge__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.visual__caption {
  margin: 0.7rem 0 0;
  color: #c7ccdd;
  text-align: center;
}

.leistungen-stack {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  padding-bottom: 1rem;
}

.stack__rail {
  position: absolute;
  inset: 0;
  left: 24px;
  width: 2px;
  background: linear-gradient(180deg, rgba(116, 227, 255, 0.4), rgba(249, 210, 112, 0.4));
  opacity: 0.4;
  box-shadow: 0 0 18px rgba(249, 210, 112, 0.4);
}

.leistung-card {
  position: relative;
  margin-left: 0.8rem;
  padding: 1.4rem 1.4rem 1.2rem 2.4rem;
  border-radius: 20px;
  background: linear-gradient(140deg, rgba(11, 12, 18, 0.98), rgba(6, 7, 11, 0.98));
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow:
    0 28px 70px rgba(0, 0, 0, 0.6),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  overflow: hidden;
  backdrop-filter: blur(6px);
  opacity: 0;
  transform: translateY(32px) scale(0.98);
  transition: transform 0.35s ease, border-color 0.25s ease, box-shadow 0.25s ease, filter 0.25s ease;
  filter: blur(12px);
}

.leistung-card::before {
  content: '';
  position: absolute;
  left: 12px;
  top: 20px;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: radial-gradient(circle, #f9d270, transparent 70%);
  box-shadow: 0 0 16px rgba(249, 210, 112, 0.75);
}

.leistung-card:hover,
.leistung-card:focus-within {
  transform: translateY(-6px) scale(1.01);
  border-color: rgba(249, 210, 112, 0.4);
  box-shadow:
    0 32px 82px rgba(0, 0, 0, 0.65),
    0 0 0 1px rgba(249, 210, 112, 0.18);
  filter: saturate(1.04);
}

.leistungen-stack .js-reveal.is-visible {
  animation: cardEnter 0.9s cubic-bezier(0.22, 0.85, 0.35, 1) forwards;
  animation-delay: var(--card-delay, 0ms);
}

.leistung-card__halo {
  position: absolute;
  inset: -24%;
  background: radial-gradient(circle at 30% 30%, rgba(249, 210, 112, 0.22), transparent 38%),
    radial-gradient(circle at 80% 60%, rgba(116, 227, 255, 0.22), transparent 42%);
  filter: blur(24px);
  opacity: 0.45;
  pointer-events: none;
}

.leistung-card__header {
  position: relative;
  display: grid;
  gap: 0.3rem;
}

.leistung-card__meta {
  display: flex;
  align-items: center;
  gap: 0.6rem;
  color: #c7cfe4;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-size: 0.82rem;
}

.leistung-card__index {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 44px;
  height: 26px;
  border-radius: 999px;
  border: 1px solid rgba(249, 210, 112, 0.45);
  background: rgba(255, 255, 255, 0.05);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.18),
    0 10px 24px rgba(0, 0, 0, 0.35);
  color: #f9d270;
  font-weight: 800;
}

.leistung-card__tag {
  padding: 0.26rem 0.7rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(116, 227, 255, 0.3);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.12),
    0 12px 28px rgba(0, 0, 0, 0.25);
}

.leistung-card h2 {
  margin: 0.15rem 0 0.3rem;
  font-size: clamp(1.5rem, 2.6vw, 1.9rem);
  letter-spacing: -0.01em;
  color: #fdf4d6;
}

.leistung-card__intro {
  margin: 0;
  color: #c9cfe0;
  line-height: 1.6;
}

.leistung-card__subline {
  margin: 0.1rem 0 0;
  color: #f9d270;
  font-weight: 700;
}

.leistung-card__list {
  margin: 0.8rem 0 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.55rem;
}

.leistung-card__item {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.6rem;
  align-items: start;
  color: #eef1f7;
  font-weight: 700;
  opacity: 0;
  transform: translateY(10px);
  filter: blur(6px);
}

.leistungen-stack .js-reveal.is-visible .leistung-card__item {
  animation: itemEnter 0.7s cubic-bezier(0.22, 0.85, 0.35, 1) forwards;
  animation-delay: calc(var(--card-delay, 0ms) + var(--item-index, 0) * 110ms + 140ms);
}

.leistung-card__icon {
  width: 26px;
  height: 26px;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.4);
  box-shadow:
    0 10px 24px rgba(0, 0, 0, 0.32),
    inset 0 1px 0 rgba(255, 255, 255, 0.16);
}

.leistung-card__shine {
  position: absolute;
  inset: 1px;
  border-radius: 19px;
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  mix-blend-mode: screen;
  opacity: 0.55;
  pointer-events: none;
}

.visual__badge,
.leistungen-hero__chip,
.leistung-card,
.leistung-card__item {
  transition: transform 0.3s ease, box-shadow 0.3s ease, filter 0.3s ease;
}

.visual__badge:hover,
.visual__badge:focus-visible,
.leistungen-hero__chip:hover,
.leistungen-hero__chip:focus-visible {
  transform: translateY(-2px);
  box-shadow:
    0 22px 50px rgba(0, 0, 0, 0.4),
    0 0 0 1px rgba(249, 210, 112, 0.22);
  filter: saturate(1.06);
}

.js-reveal {
  opacity: 0;
  transform: translateY(26px);
  transition: opacity 0.7s ease, transform 0.7s ease, filter 0.7s ease;
  transition-delay: var(--reveal-delay, 0ms);
  filter: blur(10px);
}

.js-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
  filter: blur(0);
}

@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-16px);
  }
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

@keyframes beamPulse {
  0%,
  100% {
    opacity: 0.25;
  }
  50% {
    opacity: 0.7;
  }
}

@keyframes pulse {
  0%,
  100% {
    transform: scale(0.98);
    box-shadow: 0 0 12px rgba(249, 210, 112, 0.7);
  }
  50% {
    transform: scale(1.08);
    box-shadow: 0 0 22px rgba(116, 227, 255, 0.6);
  }
}

@keyframes cardEnter {
  0% {
    opacity: 0;
    transform: translateY(34px) scale(0.96);
    filter: blur(12px);
  }
  60% {
    opacity: 1;
    transform: translateY(-6px) scale(1.01);
    filter: blur(4px);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0);
  }
}

@keyframes itemEnter {
  0% {
    opacity: 0;
    transform: translateY(12px);
    filter: blur(8px);
  }
  60% {
    opacity: 1;
    transform: translateY(-2px);
    filter: blur(3px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@media (max-width: 720px) {
  .stack__rail {
    left: 14px;
  }

  .leistung-card {
    margin-left: 0.2rem;
    padding-left: 2.2rem;
  }

  .leistungen-hero__grid {
    grid-template-columns: 1fr;
  }

  .leistungen-hero__chips {
    gap: 0.45rem;
  }
}
</style>
