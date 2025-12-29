<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

type Service = {
  badge: string
  title: string
  eyebrow: string
  summary: string
  points: string[]
  accent: 'gold' | 'cyan'
}

type Highlight = {
  label: string
  detail: string
  tone: 'gold' | 'cyan' | 'magenta'
}

const services: Service[] = [
  {
    badge: 'Lok & Traktion',
    title: 'Gestellung Triebfahrzeugführer',
    eyebrow: 'Mehrfach berechtigt',
    summary: 'Unsere Triebfahrzeugführer sind u. a. auf folgenden Baureihen berechtigt:',
    points: ['Vossloh: DE 12 · DE 18 · G1206 · G1700', 'Siemens: BR 248 Vectron Dual Mode', 'Alstom: BR 214 · BR 203 retrofit · BR 203 Handschaltrad'],
    accent: 'gold'
  },
  {
    badge: 'Rangier',
    title: 'Gestellung Rangierbegleiter',
    eyebrow: 'Bremsprobe & Wagenprüfung',
    summary:
      'Unsere Rangierbegleiter sind gleichzeitig Bremsproberechtigte, Wagenprüfer und verfügen über mehrere Jahre Erfahrung im Güter-, Nah- und Fernverkehr sowie auf Gleisbaustellen.',
    points: ['Rangierarbeiten im Güter-, Nah- und Fernverkehr', 'Rangierarbeiten im Gleisbau', 'Rangierarbeiten im Hafen', 'Rangierarbeiten in Anschlüssen'],
    accent: 'cyan'
  },
  {
    badge: 'ZbV',
    title: 'Gestellung ZbV',
    eyebrow: 'Besondere Verfügung',
    summary:
      'Unsere Mitarbeiter für die Funktion der besonderen Verfügung auf Ihren Gleisbaustellen erfüllen mindestens die Qualifikationen des Rangierbegleiters.',
    points: ['Einsatzbereit mit allen Qualifikationen des Rangierbegleiters'],
    accent: 'gold'
  },
  {
    badge: 'Wagenprüfung',
    title: 'Gestellung Wagenprüfer bis Stufe 4',
    eyebrow: 'Stufe 1–4 (ehemals Wagenmeister)',
    summary:
      'Unsere Wagenprüfer in den Stufen 1 bis 4 erfüllen mindestens die Qualifikationen des Rangierbegleiters und sind mit Stufe 3 berechtigt, Züge abzufertigen sowie die umfassenden Tätigkeiten des Wagenprüfers Stufe 4 durchzuführen.',
    points: [
      'Rangierarbeiten im Güter-, Nah- und Fernverkehr',
      'Rangierarbeiten im Gleisbau',
      'Rangierarbeiten im Hafen',
      'Rangierarbeiten in Anschlüssen',
      'Abfertigung von Zügen',
      'Erstellen von u. a. Lauffähigkeitsuntersuchungen uvm'
    ],
    accent: 'cyan'
  },
  {
    badge: 'Kippberechtigt',
    title: 'Kippwagenberechtigte',
    eyebrow: 'Spezialgeschult',
    summary:
      'Unsere Mitarbeiter für die Funktion des Kippberechtigten erfüllen mindestens die Qualifikationen des Rangierbegleiters und sind darüber hinaus explizit auf das Kippen geschult und durch eine Prüfungsbescheinigung berechtigt.',
    points: ['Geprüft und unterwiesen für das sichere Kippen auf Gleisbaustellen'],
    accent: 'gold'
  }
]

const highlights: Highlight[] = [
  {
    label: 'Audit-ready',
    detail: 'Dokumentierte Unterweisungen, Nachweise & Reporting aus einer Hand.',
    tone: 'gold'
  },
  {
    label: 'Einsatzklar in 24h',
    detail: 'Disposition, Streckenkunde & Baustellenfreigaben vorbereitet.',
    tone: 'cyan'
  },
  {
    label: 'Crew-Kontinuität',
    detail: 'Feste Teams, gleiche Gesichter, verlässlich in Schicht und Baustelle.',
    tone: 'magenta'
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
      threshold: 0.16,
      rootMargin: '0px 0px -12% 0px'
    }
  )

  revealables.forEach((element, index) => {
    element.style.setProperty('--reveal-delay', `${index * 80}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="services-page">
    <section class="services-hero js-reveal">
      <div class="services-hero__bg" aria-hidden="true">
        <div class="services-hero__grid" />
        <div class="services-hero__orb services-hero__orb--left" />
        <div class="services-hero__orb services-hero__orb--right" />
        <div class="services-hero__beam services-hero__beam--one" />
        <div class="services-hero__beam services-hero__beam--two" />
      </div>
      <div class="services-hero__content">
        <p class="eyebrow">Leistungsportfolio</p>
        <h1>Operative Teams mit Bühnenlicht-Effekt.</h1>
        <p class="services-hero__lead">
          Babylon Bahndienste liefert Lokführer, Rangierbegleiter, Wagenprüfer und Kippberechtigte mit High-End-Setup:
          dokumentiert, auditierbar, einsatzbereit. Eine Bühne voller Effekte – aber absolut verlässlich im täglichen
          Betrieb.
        </p>
        <div class="services-hero__pills">
          <span class="services-hero__pill">
            <span class="dot dot--gold" aria-hidden="true" />
            Mehrfach berechtigt
          </span>
          <span class="services-hero__pill">
            <span class="dot dot--cyan" aria-hidden="true" />
            Baustellen- und Terminal-fit
          </span>
          <span class="services-hero__pill">
            <span class="dot dot--magenta" aria-hidden="true" />
            Reporting ready
          </span>
        </div>
        <div class="services-hero__actions">
          <NuxtLink to="/kontakt" class="cta cta--solid">
            Projekt anfragen
            <span aria-hidden="true">↗</span>
          </NuxtLink>
          <NuxtLink to="/about" class="cta cta--ghost">Mehr über uns</NuxtLink>
        </div>
      </div>
      <div class="services-hero__panel">
        <p class="services-hero__panel-label">Spezialisierungen</p>
        <div class="services-hero__rail">
          <span v-for="chip in ['Lok & Traktion', 'Rangier', 'Wagenprüfung', 'Kippen']" :key="chip" class="services-hero__rail-chip">
            <span class="services-hero__rail-icon" aria-hidden="true">✧</span>
            {{ chip }}
          </span>
        </div>
        <div class="services-hero__pulse" aria-hidden="true" />
      </div>
    </section>

    <section class="highlights js-reveal">
      <div class="highlights__grid">
        <article v-for="highlight in highlights" :key="highlight.label" class="highlight-card" :class="`highlight-card--${highlight.tone}`">
          <span class="highlight-card__flare" aria-hidden="true" />
          <p class="highlight-card__label">{{ highlight.label }}</p>
          <p class="highlight-card__detail">{{ highlight.detail }}</p>
        </article>
      </div>
    </section>

    <section class="services section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Unsere Leistungen im Überblick</p>
          <h2>Alle Profile. Ein Stilvoller Auftritt.</h2>
          <p class="section__lead services__lead">
            Exakt die Leistungen aus deinem Briefing – aber in einer Bühne mit Neon-Glanzeffekt, organisierten Karten,
            animierten Linien und klaren Bullet Points.
          </p>
        </div>
      </div>

      <div class="services__grid">
        <article
          v-for="(service, index) in services"
          :key="service.title"
          class="service-card"
          :class="`service-card--${service.accent}`"
          :style="{ '--card-delay': `${index * 90}ms` }"
        >
          <div class="service-card__shine" aria-hidden="true" />
          <div class="service-card__header">
            <div class="service-card__eyeline">
              <span class="service-card__badge">{{ service.badge }}</span>
              <span class="service-card__divider" aria-hidden="true" />
              <span class="service-card__eyebrow">{{ service.eyebrow }}</span>
            </div>
            <h3>{{ service.title }}</h3>
            <p class="service-card__summary">{{ service.summary }}</p>
          </div>

          <ul class="service-card__list">
            <li v-for="point in service.points" :key="point" class="service-card__item">
              <span class="service-card__icon" aria-hidden="true">
                <span class="service-card__hex">
                  <span class="service-card__glyph">轨</span>
                </span>
              </span>
              <span class="service-card__text">{{ point }}</span>
            </li>
          </ul>

          <div class="service-card__halo" aria-hidden="true" />
        </article>
      </div>
    </section>

    <section class="cta-banner js-reveal">
      <div class="cta-banner__beam" aria-hidden="true" />
      <div>
        <p class="eyebrow">Bereit für den nächsten Umlauf?</p>
        <h2>Lasst uns das Bühnenlicht auf eure Bahnprojekte richten.</h2>
        <p class="cta-banner__lead">
          Von kurzfristigen Baustellenbesetzungen bis zu langfristigen Terminal-Betrieben: Wir bringen die Teams,
          Dokumentation und Performance-Kultur mit.
        </p>
      </div>
      <NuxtLink to="/kontakt" class="cta cta--solid cta-banner__cta">
        Kontakt aufnehmen
        <span aria-hidden="true">↗</span>
      </NuxtLink>
    </section>
  </div>
</template>

<style scoped>
.services-page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.services-hero {
  position: relative;
  overflow: hidden;
  border-radius: 28px;
  padding: clamp(1.5rem, 4vw, 2rem);
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: clamp(1.5rem, 4vw, 2.5rem);
  background: radial-gradient(circle at 12% 20%, rgba(249, 210, 112, 0.16), transparent 32%),
    radial-gradient(circle at 78% 22%, rgba(116, 227, 255, 0.14), transparent 32%),
    linear-gradient(135deg, rgba(10, 10, 14, 0.9), rgba(6, 10, 18, 0.92));
  border: 1px solid rgba(249, 210, 112, 0.3);
  box-shadow:
    0 35px 100px rgba(0, 0, 0, 0.55),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
  opacity: 0;
  transform: translateY(26px) scale(0.98);
  filter: blur(14px);
}

.services-hero.js-reveal.is-visible {
  animation: heroEnter 0.85s cubic-bezier(0.22, 0.9, 0.35, 1) forwards;
}

.services-hero__bg {
  position: absolute;
  inset: 0;
  z-index: 0;
  pointer-events: none;
}

.services-hero__grid {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.04) 1px, transparent 1px);
  background-size: 30px 30px;
  opacity: 0.3;
  mask-image: radial-gradient(circle at 40% 40%, rgba(0, 0, 0, 0.6), transparent 70%);
}

.services-hero__orb {
  position: absolute;
  width: 360px;
  height: 360px;
  border-radius: 50%;
  filter: blur(60px);
  opacity: 0.4;
}

.services-hero__orb--left {
  background: #f9d270;
  top: -80px;
  left: -120px;
}

.services-hero__orb--right {
  background: #74e3ff;
  bottom: -120px;
  right: -60px;
}

.services-hero__beam {
  position: absolute;
  inset: 0;
  background: conic-gradient(from 120deg, rgba(249, 210, 112, 0.28), rgba(10, 10, 14, 0), rgba(116, 227, 255, 0.2), rgba(10, 10, 14, 0));
  mix-blend-mode: screen;
  filter: blur(20px);
  opacity: 0.4;
}

.services-hero__beam--one {
  animation: beamSpin 24s linear infinite;
}

.services-hero__beam--two {
  animation: beamSpin 24s linear infinite reverse;
}

.services-hero__content {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 0.9rem;
  color: #f5f7ff;
}

.services-hero__lead {
  margin: 0;
  color: #cbd3e8;
  line-height: 1.6;
  max-width: 54ch;
}

.services-hero__pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 0 0 4px rgba(255, 255, 255, 0.03);
}

.dot--gold {
  background: linear-gradient(135deg, #f9d270, #c99038);
}

.dot--cyan {
  background: linear-gradient(135deg, #a7ecff, #4ad0ff);
}

.dot--magenta {
  background: linear-gradient(135deg, #ffb4f5, #d66cff);
}

.services-hero__pill {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.55rem 0.8rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(249, 210, 112, 0.2);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  color: #f1f4ff;
  font-weight: 600;
}

.services-hero__actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.services-hero__panel {
  position: relative;
  z-index: 1;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(249, 210, 112, 0.26);
  border-radius: 18px;
  padding: 1rem;
  box-shadow:
    0 20px 60px rgba(0, 0, 0, 0.5),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  overflow: hidden;
}

.services-hero__panel-label {
  margin: 0 0 0.35rem;
  color: #f6e6b4;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 0.78rem;
}

.services-hero__rail {
  display: flex;
  flex-wrap: wrap;
  gap: 0.4rem;
}

.services-hero__rail-chip {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.5rem 0.75rem;
  border-radius: 12px;
  background: rgba(6, 10, 16, 0.7);
  color: #f2f4ff;
  border: 1px solid rgba(249, 210, 112, 0.2);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08);
  font-weight: 700;
}

.services-hero__rail-icon {
  width: 20px;
  height: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: linear-gradient(135deg, rgba(249, 210, 112, 0.85), rgba(116, 227, 255, 0.8));
  color: #0a0b0f;
  font-size: 0.75rem;
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.35);
}

.services-hero__pulse {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 50% 50%, rgba(249, 210, 112, 0.08), transparent 50%);
  animation: pulse 3.2s ease-in-out infinite;
  pointer-events: none;
}

.services-hero__panel::after {
  content: '';
  position: absolute;
  inset: 1px;
  border-radius: 16px;
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0));
  opacity: 0.7;
  pointer-events: none;
}

.highlights {
  background: rgba(255, 255, 255, 0.03);
  border-radius: 20px;
  padding: clamp(1rem, 2vw, 1.4rem);
  border: 1px solid rgba(249, 210, 112, 0.16);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.04);
  opacity: 0;
  transform: translateY(18px);
  filter: blur(10px);
}

.highlights.js-reveal.is-visible {
  animation: fadeUp 0.8s ease forwards;
}

.highlights__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 0.8rem;
}

.highlight-card {
  position: relative;
  padding: 0.95rem 1rem;
  border-radius: 14px;
  border: 1px solid rgba(255, 255, 255, 0.06);
  background: rgba(0, 0, 0, 0.35);
  overflow: hidden;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06);
}

.highlight-card__label {
  margin: 0;
  font-weight: 800;
  letter-spacing: 0.03em;
}

.highlight-card__detail {
  margin: 0.25rem 0 0;
  color: #d8dff2;
  line-height: 1.5;
}

.highlight-card__flare {
  position: absolute;
  inset: -40%;
  background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.12), transparent 52%);
  filter: blur(20px);
  opacity: 0.5;
  pointer-events: none;
}

.highlight-card--gold {
  border-color: rgba(249, 210, 112, 0.3);
}

.highlight-card--gold .highlight-card__label {
  color: #f9d270;
}

.highlight-card--cyan {
  border-color: rgba(116, 227, 255, 0.28);
}

.highlight-card--cyan .highlight-card__label {
  color: #a7ecff;
}

.highlight-card--magenta {
  border-color: rgba(243, 152, 255, 0.3);
}

.highlight-card--magenta .highlight-card__label {
  color: #ffcff7;
}

.services__lead {
  max-width: 68ch;
}

.services__grid {
  margin-top: 1.5rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1rem;
}

.service-card {
  position: relative;
  background: linear-gradient(150deg, rgba(14, 14, 20, 0.9), rgba(8, 8, 12, 0.96));
  border-radius: 18px;
  padding: 1.2rem 1.15rem 1.1rem;
  border: 1px solid rgba(249, 210, 112, 0.2);
  box-shadow:
    0 22px 60px rgba(0, 0, 0, 0.5),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
  overflow: hidden;
  opacity: 0;
  transform: translateY(20px) scale(0.98);
  filter: blur(12px);
  color: #f5f7ff;
}

.services.section.js-reveal.is-visible .service-card {
  animation: cardEnter 0.85s cubic-bezier(0.22, 0.9, 0.35, 1) forwards;
  animation-delay: var(--card-delay);
}

.service-card--cyan {
  border-color: rgba(116, 227, 255, 0.28);
}

.service-card__shine {
  position: absolute;
  inset: -20%;
  background: conic-gradient(
    from 120deg,
    rgba(249, 210, 112, 0.18),
    rgba(0, 0, 0, 0),
    rgba(116, 227, 255, 0.2),
    rgba(0, 0, 0, 0)
  );
  mix-blend-mode: screen;
  filter: blur(24px);
  opacity: 0.6;
  animation: beamSpin 18s linear infinite;
}

.service-card__header {
  position: relative;
  display: grid;
  gap: 0.3rem;
}

.service-card__eyeline {
  display: grid;
  grid-template-columns: auto 1fr auto;
  gap: 0.5rem;
  align-items: center;
  color: #c8d1e9;
  letter-spacing: 0.08em;
  font-size: 0.78rem;
  text-transform: uppercase;
}

.service-card__badge {
  padding: 0.26rem 0.55rem;
  border-radius: 999px;
  border: 1px solid rgba(249, 210, 112, 0.3);
  background: rgba(255, 255, 255, 0.05);
  font-weight: 800;
}

.service-card__divider {
  height: 1px;
  background: linear-gradient(90deg, rgba(249, 210, 112, 0.4), rgba(116, 227, 255, 0.5));
  opacity: 0.7;
}

.service-card__eyebrow {
  justify-self: end;
}

.service-card h3 {
  margin: 0;
  font-size: 1.2rem;
}

.service-card__summary {
  margin: 0;
  color: #d6dcf0;
  line-height: 1.55;
}

.service-card__list {
  margin: 0.75rem 0 0;
  padding: 0;
  display: grid;
  gap: 0.5rem;
  list-style: none;
}

.service-card__item {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.6rem;
  align-items: start;
}

.service-card__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.service-card__hex {
  width: 40px;
  height: 40px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #f9d270, #c99038);
  clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%);
  box-shadow:
    0 12px 26px rgba(0, 0, 0, 0.35),
    inset 0 1px 0 rgba(255, 255, 255, 0.2);
}

.service-card__glyph {
  font-size: 1.05rem;
  color: #040405;
  font-weight: 900;
}

.service-card__text {
  line-height: 1.5;
  color: #eef2ff;
}

.service-card__halo {
  position: absolute;
  inset: -10%;
  background: radial-gradient(circle at 22% 26%, rgba(249, 210, 112, 0.06), transparent 42%),
    radial-gradient(circle at 80% 70%, rgba(116, 227, 255, 0.06), transparent 42%);
  opacity: 0.6;
  filter: blur(8px);
  pointer-events: none;
  animation: pulse 4s ease-in-out infinite;
}

.service-card:hover,
.service-card:focus-within {
  transform: translateY(-6px) scale(1.01);
  border-color: rgba(249, 210, 112, 0.35);
  box-shadow:
    0 28px 80px rgba(0, 0, 0, 0.6),
    0 0 0 1px rgba(249, 210, 112, 0.2);
}

.cta-banner {
  position: relative;
  overflow: hidden;
  border-radius: 20px;
  padding: clamp(1.3rem, 2.5vw, 1.8rem);
  background: linear-gradient(140deg, rgba(249, 210, 112, 0.16), rgba(12, 12, 18, 0.9)),
    radial-gradient(circle at 18% 20%, rgba(255, 255, 255, 0.08), transparent 42%),
    #0a0a10;
  border: 1px solid rgba(249, 210, 112, 0.22);
  box-shadow:
    0 24px 70px rgba(0, 0, 0, 0.55),
    inset 0 1px 0 rgba(255, 255, 255, 0.04);
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 1rem;
  align-items: center;
  opacity: 0;
  transform: translateY(16px);
  filter: blur(10px);
}

.cta-banner.js-reveal.is-visible {
  animation: fadeUp 0.9s ease forwards;
}

.cta-banner__lead {
  margin: 0.4rem 0 0;
  color: #d4dcf3;
  line-height: 1.6;
}

.cta-banner__cta {
  justify-self: end;
}

.cta-banner__beam {
  position: absolute;
  inset: 0;
  background: conic-gradient(
    from 200deg,
    rgba(249, 210, 112, 0.25),
    rgba(0, 0, 0, 0),
    rgba(116, 227, 255, 0.18),
    rgba(0, 0, 0, 0)
  );
  mix-blend-mode: screen;
  opacity: 0.6;
  pointer-events: none;
  filter: blur(18px);
  animation: beamSpin 26s linear infinite;
}

@keyframes heroEnter {
  0% {
    opacity: 0;
    transform: translateY(26px) scale(0.98);
    filter: blur(14px);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0);
  }
}

@keyframes beamSpin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes pulse {
  0%,
  100% {
    opacity: 0.55;
    transform: scale(1);
  }
  50% {
    opacity: 0.9;
    transform: scale(1.05);
  }
}

@keyframes fadeUp {
  0% {
    opacity: 0;
    transform: translateY(18px);
    filter: blur(10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
    filter: blur(0);
  }
}

@keyframes cardEnter {
  0% {
    opacity: 0;
    transform: translateY(20px) scale(0.98);
    filter: blur(12px);
  }
  60% {
    transform: translateY(-4px) scale(1.01);
    filter: blur(3px);
  }
  100% {
    opacity: 1;
    transform: translateY(0) scale(1);
    filter: blur(0);
  }
}

@media (max-width: 820px) {
  .services-hero__actions {
    flex-direction: column;
    align-items: stretch;
  }

  .cta-banner {
    grid-template-columns: 1fr;
  }

  .cta-banner__cta {
    justify-self: start;
  }
}
</style>
