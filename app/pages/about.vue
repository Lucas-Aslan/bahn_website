<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

type Pillar = {
  badge: string
  title: string
  description: string
}

type Milestone = {
  year: string
  title: string
  detail: string
}

type FocusArea = {
  label: string
  detail: string
}

type ImageModule = {
  title: string
  caption: string
  src: string
  accent: 'gold' | 'cyan'
}

const pillars: Pillar[] = [
  {
    badge: '01',
    title: 'Einsatzklar in 24h',
    description:
      'Disposition, Streckenkunde und Unterweisungen werden in der Leitstelle vorbereitet. So stellen wir Crews schnell und auditierbar.'
  },
  {
    badge: '02',
    title: 'Sicherheitsführend',
    description:
      'Dokumentierte Unterweisungen, Risikobeurteilungen und Reporting nach EBA-Standard – für Baustelle, Cargo und Terminal.'
  },
  {
    badge: '03',
    title: 'Partnerschaftlich',
    description:
      'Feste Ansprechpartner, proaktive Kommunikation und transparente KPIs, damit Projekte auf der Schiene planbar bleiben.'
  }
]


const focusAreas: FocusArea[] = [
  {
    label: 'Lok & Traktion',
    detail: 'Mehrfach berechtigte Triebfahrzeugführer inkl. Streckenkunde und Baustellenberechtigungen.'
  },
  {
    label: 'Rangier & Wagenprüfung',
    detail: 'Bremsproben, Wagenprüfungen bis Stufe 4, Kippberechtigte – dokumentiert und einsatzklar.'
  },
  {
    label: 'Disposition & Reporting',
    detail: 'Crew-Planung, Statusmeldungen und Tagesreports mit klaren KPIs für stabile Umläufe.'
  }
]

const imageModules: ImageModule[] = [
  {
    title: 'Einsatzteams in Aktion',
    caption: 'Platzhalter für dein starkes Einsatzbild. Wir koordinieren Crews, sichern Strecken und halten Termine.',
    src: '/images/cta-bild.jpg',
    accent: 'gold'
  },
  {
    title: 'Digitale Leitstelle',
    caption:
      'Hier kann dein Leitstellen- oder Dashboard-Visual hin. Wir steuern, dokumentieren und reporten zentral.',
    src: '/images/ops-desk-visual.svg',
    accent: 'cyan'
  }
]

const scrollY = ref(0)
const heroDrift = computed(() => Math.min(scrollY.value * 0.12, 60))
const orbitSpin = computed(() => Math.min(scrollY.value * 0.08, 48))
let revealObserver: IntersectionObserver | null = null

const handleScroll = () => {
  scrollY.value = window.scrollY
}

onMounted(() => {
  scrollY.value = window.scrollY
  window.addEventListener('scroll', handleScroll, { passive: true })

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
    element.style.setProperty('--reveal-delay', `${index * 70}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll)
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="about-page">
    <section class="about-hero">
      <div class="about-hero__bg" aria-hidden="true">
        <div class="about-hero__beam about-hero__beam--one" :style="{ transform: `translateY(${heroDrift}px)` }" />
        <div class="about-hero__beam about-hero__beam--two" :style="{ transform: `translateY(${heroDrift * -0.4}px)` }" />
        <div class="about-hero__ring about-hero__ring--gold" :style="{ transform: `rotate(${orbitSpin}deg)` }" />
        <div class="about-hero__ring about-hero__ring--cyan" :style="{ transform: `rotate(${orbitSpin * -1.2}deg)` }" />
      </div>

      <div class="about-hero__grid">
        <div class="about-hero__content js-reveal">
          <p class="eyebrow">Über Babylon Bahndienste</p>
          <h1>Wir halten Bahndienste planbar, sicher und messbar.</h1>
          <p class="about-hero__lead">
            Unsere Teams sichern Bau, Cargo, Terminal und Hafenlogistik – mit klaren Prozessen, 24/7-Disposition und
            revisionssicherer Dokumentation. So bleiben Umläufe stabil und Audits stressfrei.
          </p>
          <div class="about-hero__highlights">
            <div class="about-hero__chip">
              <span class="dot dot--gold" aria-hidden="true" />
              Einsatzsteuerung & Reporting
            </div>
            <div class="about-hero__chip">
              <span class="dot dot--cyan" aria-hidden="true" />
              Triebfahrzeugführer, Rangierbegleiter & Wagenprüfer
            </div>
          </div>
          <div class="about-hero__actions">
            <NuxtLink to="/kontakt" class="cta cta--solid">
              Anfrage starten
              <span aria-hidden="true">↗</span>
            </NuxtLink>
            <NuxtLink to="/leistungen/transport" class="cta cta--ghost">Leistungen ansehen</NuxtLink>
          </div>
        </div>

        <div class="about-hero__visual js-reveal">
          <div class="about-hero__image-frame">
            <img
              src="/images/cta-bild.jpg"
              alt="Crew von Babylon Bahndiensten koordiniert einen Einsatz"
              class="about-hero__image"
              loading="lazy"
            >
            <div class="about-hero__image-overlay" aria-hidden="true" />
            <div class="about-hero__image-badge">
              <span class="dot dot--magenta" aria-hidden="true" />
              Einsatzbereit in 24h
            </div>
          </div>
          <p class="about-hero__visual-copy">
            Wir stellen einsatzbereite Teams, sichern Strecken und dokumentieren jeden Schritt – damit dein Betrieb
            stabil bleibt.
          </p>
        </div>
      </div>
    </section>

    <section class="pillars section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Unser Auftrag</p>
          <h2>Babylon DNA</h2>
          <p class="section__lead">
            Wir kombinieren operative Präzision, Sicherheit und partnerschaftliche Steuerung. Die folgenden Prinzipien
            leiten jedes Projekt.
          </p>
        </div>
      </div>
      <div class="pillars__grid">
        <article v-for="pillar in pillars" :key="pillar.title" class="pillar-card">
          <span class="pillar-card__badge">{{ pillar.badge }}</span>
          <h3>{{ pillar.title }}</h3>
          <p>{{ pillar.description }}</p>
          <span class="pillar-card__glow" aria-hidden="true" />
        </article>
      </div>
    </section>

    <section class="focus section js-reveal">
      <div class="focus__grid">
        <div class="focus__intro">
          <p class="eyebrow">Fokusfelder</p>
          <h2>Operativ stark. Beratend präzise.</h2>
          <p class="section__lead">
            Egal ob Baukorridor, Terminal oder Hafen: Wir bringen qualifiziertes Personal, zentrale Einsatzsteuerung und
            Compliance-Erfahrung mit.
          </p>
          <div class="focus__badges">
            <span class="badge badge--gold">Sicherungslogik</span>
            <span class="badge badge--cyan">Dokumentiert</span>
            <span class="badge badge--magenta">Auditbereit</span>
          </div>
        </div>
        <div class="focus__cards">
          <article v-for="area in focusAreas" :key="area.label" class="focus-card">
            <div class="focus-card__header">
              <span class="focus-card__marker" aria-hidden="true">✦</span>
              <p class="focus-card__label">{{ area.label }}</p>
            </div>
            <p class="focus-card__detail">{{ area.detail }}</p>
            <span class="focus-card__glow" aria-hidden="true" />
          </article>
        </div>
      </div>
    </section>

    <section class="visuals section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Bildmodule</p>
          <h2>Starke Bilder für deine Projekte</h2>
          <p class="section__lead">
            Füge hier eigene Motive ein – ob Einsatzteams, Leitstelle oder Bahninfrastruktur. Overlays und Captions sind
            bereits vorbereitet.
          </p>
        </div>
      </div>
      <div class="visuals__grid">
        <figure
          v-for="module in imageModules"
          :key="module.title"
          class="visual-card"
          :data-accent="module.accent"
        >
          <div class="visual-card__frame">
            <img :src="module.src" :alt="module.title" loading="lazy">
            <div class="visual-card__overlay" aria-hidden="true" />
          </div>
          <figcaption class="visual-card__caption">
            <p class="visual-card__title">{{ module.title }}</p>
            <p class="visual-card__text">{{ module.caption }}</p>
          </figcaption>
          <span class="visual-card__pulse" aria-hidden="true" />
        </figure>
      </div>
    </section>

    <section class="gold-cta section js-reveal">
      <div class="gold-cta__grid">
        <figure class="gold-cta__media">
          <img
            src="/images/cta-bild.jpg"
            alt="Einsatzkoordination und Crew-Übersicht von Babylon Bahndiensten"
            class="gold-cta__image"
            loading="lazy"
          >
          <figcaption class="gold-cta__legend">
            <span class="gold-cta__legend-dot" aria-hidden="true" />
            Einsatzkoordination &amp; Sicherheit im Blick
          </figcaption>
        </figure>

        <div class="gold-cta__content">
          <p class="gold-cta__eyebrow">Babylon Bahndienste</p>
          <h2>Wir stellen Crews, sichern Strecken und liefern Reporting.</h2>
          <p class="gold-cta__lead">
            Von Traktion über Rangier bis Wagenprüfung – wir starten schnell, steuern zentral und halten Sie mit
            belastbaren KPIs auf dem Laufenden.
          </p>
          <div class="gold-cta__actions">
            <NuxtLink to="/kontakt" class="gold-cta__button gold-cta__button--solid">
              Kontaktieren
              <span aria-hidden="true">↗</span>
            </NuxtLink>
            <NuxtLink to="/leistungen/transport" class="gold-cta__button gold-cta__button--ghost">
              Leistungen entdecken
              <span aria-hidden="true">↗</span>
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.about-page {
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.35rem 0.75rem;
  border-radius: 999px;
  background: linear-gradient(120deg, rgba(249, 210, 112, 0.12), rgba(255, 255, 255, 0.04));
  color: #f6e6b4;
  font-weight: 700;
  letter-spacing: 0.02em;
}

.section {
  position: relative;
  width: min(1100px, 94vw);
  margin: 0 auto;
  padding: 1rem 0 0;
}

.section__header {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 1rem;
  margin-bottom: 1.2rem;
}

.section__lead {
  margin: 0.6rem 0 0;
  color: #cfe2ff;
  line-height: 1.6;
  max-width: 680px;
}

h1,
h2 {
  margin: 0.25rem 0;
  letter-spacing: -0.02em;
}

.about-hero {
  position: relative;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  padding: clamp(2rem, 6vw, 3rem) clamp(1.5rem, 4vw, 3rem) clamp(2.5rem, 6vw, 3.4rem);
  background: radial-gradient(circle at 18% 12%, rgba(249, 210, 112, 0.12), transparent 32%),
    radial-gradient(circle at 80% 10%, rgba(80, 196, 255, 0.12), transparent 30%),
    linear-gradient(135deg, rgba(6, 10, 20, 0.94), rgba(2, 6, 14, 0.9));
  overflow: hidden;
  border-radius: 0 0 24px 24px;
  box-shadow: 0 40px 110px rgba(0, 0, 0, 0.55), inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.about-hero__grid {
  position: relative;
  z-index: 1;
  max-width: 1100px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: clamp(1.2rem, 4vw, 2rem);
  align-items: center;
}

.about-hero__bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
}

.about-hero__beam {
  position: absolute;
  inset: 8% 6%;
  filter: blur(28px);
  opacity: 0.45;
  mix-blend-mode: screen;
  animation: beamShift 8s ease-in-out infinite alternate;
}

.about-hero__beam--one {
  background: radial-gradient(circle at 20% 30%, rgba(249, 210, 112, 0.35), transparent 40%),
    radial-gradient(circle at 70% 10%, rgba(12, 160, 255, 0.25), transparent 35%);
}

.about-hero__beam--two {
  background: radial-gradient(circle at 80% 70%, rgba(96, 240, 200, 0.28), transparent 32%),
    radial-gradient(circle at 30% 78%, rgba(249, 210, 112, 0.2), transparent 38%);
}

.about-hero__ring {
  position: absolute;
  width: 58%;
  aspect-ratio: 1 / 1;
  border-radius: 50%;
  left: 22%;
  top: 6%;
  filter: drop-shadow(0 24px 60px rgba(0, 0, 0, 0.4));
  opacity: 0.32;
  animation: slowSpin 18s linear infinite;
}

.about-hero__ring--gold {
  border: 1px solid rgba(249, 210, 112, 0.42);
  box-shadow: 0 0 80px rgba(249, 210, 112, 0.18);
}

.about-hero__ring--cyan {
  border: 1px solid rgba(80, 196, 255, 0.35);
  transform-origin: center;
  animation-duration: 22s;
}

.about-hero__content {
  display: grid;
  gap: 1rem;
}

.about-hero__lead {
  margin: 0;
  max-width: 820px;
  color: #d7e8ff;
  line-height: 1.65;
  font-size: 1.05rem;
}

.about-hero__highlights {
  display: flex;
  flex-wrap: wrap;
  gap: 0.65rem;
}

.about-hero__chip {
  display: inline-flex;
  align-items: center;
  gap: 0.55rem;
  padding: 0.65rem 0.9rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: #e8f0ff;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  display: inline-block;
  box-shadow: 0 0 15px currentColor;
}

.dot--gold {
  background: #f9d270;
  color: #f9d270;
}

.dot--cyan {
  background: #5ad2ff;
  color: #5ad2ff;
}

.dot--magenta {
  background: #ff7ad5;
  color: #ff7ad5;
}

.about-hero__actions {
  display: flex;
  gap: 0.7rem;
  flex-wrap: wrap;
}

.cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.9rem 1.2rem;
  border-radius: 12px;
  font-weight: 700;
  text-decoration: none;
  color: #0c0c0c;
  background: linear-gradient(120deg, #f9d270, #c99038);
  box-shadow: 0 14px 40px rgba(249, 210, 112, 0.3);
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
}

.cta--ghost {
  background: transparent;
  color: #e8f0ff;
  border: 1px solid rgba(255, 255, 255, 0.12);
  box-shadow: none;
}

.cta:hover,
.cta:focus-visible {
  transform: translateY(-2px);
  box-shadow: 0 18px 50px rgba(249, 210, 112, 0.35);
}

.cta--ghost:hover,
.cta--ghost:focus-visible {
  box-shadow: 0 18px 40px rgba(255, 255, 255, 0.12);
}

.about-hero__visual {
  display: grid;
  gap: 0.7rem;
}

.about-hero__image-frame {
  position: relative;
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.08);
  background: rgba(0, 0, 0, 0.35);
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.5);
  isolation: isolate;
}

.about-hero__image {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
  filter: saturate(1.05) contrast(1.03);
}

.about-hero__image-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.05), rgba(0, 0, 0, 0.55));
}

.about-hero__image-badge {
  position: absolute;
  left: 12px;
  bottom: 12px;
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.55rem 0.75rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.7);
  color: #fcecff;
  font-weight: 700;
  letter-spacing: 0.01em;
}

.about-hero__visual-copy {
  margin: 0;
  color: #dfeeff;
  line-height: 1.6;
  max-width: 520px;
}

.about-hero__meta {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 0.8rem;
  margin-top: 0.4rem;
}

.meta-card {
  padding: 0.9rem 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06);
}

.meta-card__value {
  margin: 0;
  font-size: 1.4rem;
  font-weight: 800;
  letter-spacing: -0.01em;
}

.meta-card__label {
  margin: 0.25rem 0 0;
  color: #cfe2ff;
}

.pillars__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
}

.pillar-card {
  position: relative;
  padding: 1rem;
  border-radius: 16px;
  background: linear-gradient(160deg, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.02));
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 22px 60px rgba(0, 0, 0, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.05);
  overflow: hidden;
  min-height: 210px;
}

.pillar-card__badge {
  display: inline-flex;
  padding: 0.35rem 0.65rem;
  border-radius: 12px;
  background: rgba(249, 210, 112, 0.12);
  color: #f9d270;
  font-weight: 800;
  letter-spacing: 0.02em;
}

.pillar-card h3 {
  margin: 0.5rem 0 0.35rem;
  letter-spacing: -0.01em;
}

.pillar-card p {
  margin: 0;
  color: #cfe2ff;
  line-height: 1.55;
}

.pillar-card__glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 10%, rgba(249, 210, 112, 0.16), transparent 40%),
    radial-gradient(circle at 80% 80%, rgba(80, 196, 255, 0.15), transparent 35%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.pillar-card:hover .pillar-card__glow,
.pillar-card:focus-within .pillar-card__glow {
  opacity: 1;
}

.milestones {
  overflow: hidden;
}

.milestones__track {
  position: absolute;
  left: 24px;
  top: 108px;
  bottom: 0;
  width: 2px;
  background: linear-gradient(180deg, rgba(249, 210, 112, 0.65), rgba(80, 196, 255, 0.5));
  border-radius: 999px;
}

.milestones__list {
  display: grid;
  gap: 1.2rem;
  margin-top: 0.5rem;
}

.milestone {
  display: grid;
  grid-template-columns: 70px 1fr;
  gap: 1rem;
  align-items: start;
  padding: 0.8rem 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.35);
}

.milestone__time {
  position: relative;
  display: grid;
  place-items: center;
}

.milestone__year {
  font-weight: 800;
  color: #f9d270;
  letter-spacing: 0.02em;
}

.milestone__pulse {
  position: absolute;
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: #f9d270;
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.45);
  animation: pulse 2.8s infinite;
}

.milestone__content h3 {
  margin: 0;
}

.milestone__content p {
  margin: 0.3rem 0 0;
  color: #cfe2ff;
  line-height: 1.55;
}

.focus__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: 1.2rem;
  align-items: start;
}

.focus__badges {
  display: flex;
  gap: 0.4rem;
  flex-wrap: wrap;
  margin-top: 0.6rem;
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.5rem 0.75rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.08);
  font-weight: 700;
}

.badge::before {
  content: '';
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: currentColor;
  box-shadow: 0 0 12px currentColor;
}

.badge--gold {
  color: #f9d270;
}

.badge--cyan {
  color: #5ad2ff;
}

.badge--magenta {
  color: #ff7ad5;
}

.focus__cards {
  display: grid;
  gap: 0.9rem;
}

.focus-card {
  position: relative;
  padding: 1rem;
  border-radius: 14px;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.04), rgba(255, 255, 255, 0.02));
  border: 1px solid rgba(255, 255, 255, 0.06);
  overflow: hidden;
}

.focus-card__header {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.focus-card__marker {
  width: 28px;
  height: 28px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  border: 1px solid rgba(249, 210, 112, 0.2);
  color: #f9d270;
  background: rgba(249, 210, 112, 0.08);
}

.focus-card__label {
  margin: 0;
  font-weight: 700;
}

.focus-card__detail {
  margin: 0.35rem 0 0;
  color: #cfe2ff;
  line-height: 1.6;
}

.focus-card__glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 40% 0%, rgba(249, 210, 112, 0.18), transparent 40%),
    radial-gradient(circle at 90% 90%, rgba(80, 196, 255, 0.16), transparent 35%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.focus-card:hover .focus-card__glow,
.focus-card:focus-within .focus-card__glow {
  opacity: 1;
}

.visuals__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1rem;
}

.visual-card {
  position: relative;
  border-radius: 18px;
  overflow: hidden;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 20px 70px rgba(0, 0, 0, 0.45);
  isolation: isolate;
}

.visual-card__frame {
  position: relative;
  overflow: hidden;
  max-height: 360px;
}

.visual-card img {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
  filter: saturate(1.08) contrast(1.04);
}

.visual-card__overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(180deg, transparent, rgba(6, 8, 16, 0.8));
}

.visual-card__caption {
  padding: 1rem;
  display: grid;
  gap: 0.2rem;
}

.visual-card__title {
  margin: 0;
  font-weight: 800;
  letter-spacing: -0.01em;
}

.visual-card__text {
  margin: 0;
  color: #d7e8ff;
  line-height: 1.5;
}

.visual-card__pulse {
  position: absolute;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  right: 14px;
  top: 14px;
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.4);
  animation: pulse 3.2s infinite;
}

.visual-card[data-accent='gold'] .visual-card__pulse {
  background: #f9d270;
}

.visual-card[data-accent='cyan'] .visual-card__pulse {
  background: #5ad2ff;
}

.gold-cta {
  width: min(1100px, 94vw);
  margin: 0 auto 1.5rem;
}

.gold-cta__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  align-items: center;
  padding: 1rem;
  border-radius: 22px;
  background: linear-gradient(130deg, rgba(249, 210, 112, 0.12), rgba(12, 16, 28, 0.92));
  border: 1px solid rgba(249, 210, 112, 0.18);
  box-shadow: 0 28px 80px rgba(0, 0, 0, 0.5), inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.gold-cta__media {
  position: relative;
  border-radius: 18px;
  overflow: hidden;
  margin: 0;
  border: 1px solid rgba(255, 255, 255, 0.08);
  background: rgba(0, 0, 0, 0.3);
}

.gold-cta__image {
  width: 100%;
  height: 100%;
  display: block;
  object-fit: cover;
}

.gold-cta__legend {
  position: absolute;
  left: 12px;
  bottom: 12px;
  padding: 0.45rem 0.65rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.6);
  color: #e8f0ff;
  display: inline-flex;
  gap: 0.5rem;
  align-items: center;
}

.gold-cta__legend-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f9d270;
  box-shadow: 0 0 12px rgba(249, 210, 112, 0.7);
}

.gold-cta__content h2 {
  margin-top: 0.15rem;
}

.gold-cta__lead {
  margin: 0.5rem 0 0.6rem;
  color: #f8f6ee;
  line-height: 1.6;
}

.gold-cta__actions {
  display: flex;
  gap: 0.7rem;
  flex-wrap: wrap;
}

.gold-cta__button {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.85rem 1.1rem;
  border-radius: 12px;
  font-weight: 800;
  text-decoration: none;
}

.gold-cta__button--solid {
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0c0c;
  box-shadow: 0 18px 50px rgba(249, 210, 112, 0.35);
}

.gold-cta__button--ghost {
  border: 1px solid rgba(255, 255, 255, 0.12);
  color: #e8f0ff;
}

.js-reveal {
  opacity: 0;
  transform: translateY(16px);
  filter: blur(4px);
  transition: opacity 0.4s ease, transform 0.4s ease, filter 0.4s ease;
  transition-delay: var(--reveal-delay, 0ms);
}

.js-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
  filter: blur(0);
}

@keyframes slowSpin {
  to {
    transform: rotate(360deg);
  }
}

@keyframes beamShift {
  from {
    transform: translateY(-12px);
  }
  to {
    transform: translateY(12px);
  }
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.4);
  }
  70% {
    box-shadow: 0 0 0 18px rgba(249, 210, 112, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0);
  }
}

@media (max-width: 900px) {
  .section__header {
    flex-direction: column;
    align-items: flex-start;
  }

  .milestone {
    grid-template-columns: 1fr;
  }

  .milestones__track {
    left: 12px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .about-hero__beam,
  .about-hero__ring,
  .visual-card__pulse,
  .milestone__pulse {
    animation: none;
  }
}
</style>
