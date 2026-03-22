<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

type Pillar = {
  title: string
  description: string
}

type FocusArea = {
  label: string
  detail: string
}

type ImageModule = {
  title: string
  caption: string
  src: string
}

const pillars: Pillar[] = [
  {
    title: 'Einsatzklar in 24h',
    description:
      'Disposition, Streckenkunde und Unterweisungen werden in der Leitstelle vorbereitet. So stellen wir Crews schnell und auditierbar.'
  },
  {
    title: 'Sicherheitsführend',
    description:
      'Dokumentierte Unterweisungen, Risikobeurteilungen und Reporting nach EBA-Standard – für Baustelle, Cargo und Terminal.'
  },
  {
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
    caption: 'Wir koordinieren Crews, sichern Strecken und halten Termine verlässlich ein.',
    src: '/images/cta-bild.jpg'
  },
  {
    title: 'Digitale Leitstelle',
    caption: 'Zentrale Einsatzsteuerung mit nachvollziehbarer Dokumentation und transparentem Reporting.',
    src: '/images/ops-desk-visual.svg'
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
      threshold: 0.2,
      rootMargin: '0px 0px -10% 0px'
    }
  )

  revealables.forEach((element, index) => {
    element.style.setProperty('--reveal-delay', `${index * 70}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="about-page">
    <section class="about-hero section js-reveal">
      <div class="about-hero__content">
        <p class="eyebrow">Über Babylon Bahndienste</p>
        <h1>Wir halten Bahndienste planbar, sicher und messbar.</h1>
        <p class="section__lead">
          Unsere Teams sichern Bau, Cargo, Terminal und Hafenlogistik – mit klaren Prozessen, 24/7-Disposition und
          revisionssicherer Dokumentation. So bleiben Umläufe stabil und Audits stressfrei.
        </p>
        <div class="about-hero__actions">
          <NuxtLink to="/kontakt" class="cta cta--solid">Anfrage starten</NuxtLink>
          <NuxtLink to="/leistungen" class="cta cta--ghost">Leistungen ansehen</NuxtLink>
        </div>
      </div>
      <div class="about-hero__image-wrap">
        <img
          src="/images/cta-bild.jpg"
          alt="Crew von Babylon Bahndiensten koordiniert einen Einsatz"
          class="about-hero__image"
          loading="lazy"
        >
      </div>
    </section>

    <section class="section js-reveal">
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
      <div class="card-grid">
        <article v-for="pillar in pillars" :key="pillar.title" class="info-card">
          <h3>{{ pillar.title }}</h3>
          <p>{{ pillar.description }}</p>
        </article>
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header section__header--split">
        <div>
          <p class="eyebrow">Fokusfelder</p>
          <h2>Operativ stark. Beratend präzise.</h2>
          <p class="section__lead">
            Egal ob Baukorridor, Terminal oder Hafen: Wir bringen qualifiziertes Personal, zentrale Einsatzsteuerung und
            Compliance-Erfahrung mit.
          </p>
        </div>
        <NuxtLink to="/kontakt" class="cta cta--solid">Projekt besprechen</NuxtLink>
      </div>
      <div class="card-grid">
        <article v-for="area in focusAreas" :key="area.label" class="info-card">
          <p class="card-meta">{{ area.label }}</p>
          <p>{{ area.detail }}</p>
        </article>
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Einblicke</p>
          <h2>Starke Bilder für starke Einsätze</h2>
          <p class="section__lead">
            Ob Einsatzteams, Leitstelle oder Bahninfrastruktur: So sieht Zusammenarbeit mit Babylon Bahndienste aus.
          </p>
        </div>
      </div>
      <div class="visual-grid">
        <figure v-for="module in imageModules" :key="module.title" class="visual-card">
          <img :src="module.src" :alt="module.title" loading="lazy">
          <figcaption>
            <h3>{{ module.title }}</h3>
            <p>{{ module.caption }}</p>
          </figcaption>
        </figure>
      </div>
    </section>

    <section class="section section--cta js-reveal">
      <div>
        <p class="eyebrow">Zusammenarbeit</p>
        <h2>Wir stellen Crews, sichern Strecken und liefern Reporting.</h2>
        <p class="section__lead">
          Von Traktion über Rangier bis Wagenprüfung – wir starten schnell, steuern zentral und halten Sie mit
          belastbaren KPIs auf dem Laufenden.
        </p>
      </div>
      <NuxtLink to="/kontakt" class="cta cta--solid">Kontaktieren</NuxtLink>
    </section>
  </div>
</template>

<style scoped>
.about-page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.section {
  background: transparent;
  border-radius: 24px;
  padding: clamp(1.5rem, 2vw, 2rem);
}

.section__header {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 260px), 1fr));
  gap: 1.4rem;
  align-items: end;
  margin-bottom: 1rem;
}

.section__header--split {
  align-items: center;
}

h2 {
  margin: 0.2rem 0 0.35rem;
  font-size: clamp(1.8rem, 3vw, 2.3rem);
  letter-spacing: -0.01em;
  color: var(--color-forest);
}

.section__lead {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.6;
}

.eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--color-rose);
  font-size: 0.82rem;
  background: rgba(11, 122, 92, 0.12);
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  display: inline-flex;
}

.cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.85rem 1.2rem;
  border-radius: 12px;
  font-weight: 700;
  letter-spacing: 0.01em;
  text-decoration: none;
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
  border: 1px solid transparent;
}

.cta--solid {
  background: var(--color-rose);
  color: #ffffff;
  box-shadow: 0 18px 45px rgba(11, 122, 92, 0.28);
}

.cta--ghost {
  background: var(--color-rose);
  color: #ffffff;
  border-color: rgba(11, 122, 92, 0.35);
}

.cta:hover,
.cta:focus-visible {
  transform: translateY(-1px);
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

.about-hero {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(11, 122, 92, 0.12), rgba(47, 52, 57, 0.08));
  border-radius: 24px;
}

.about-hero__content h1 {
  margin: 0.2rem 0 0.45rem;
  font-size: clamp(2rem, 3vw, 2.6rem);
  color: var(--color-forest);
}

.about-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1rem;
}

.about-hero__image-wrap {
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid var(--color-border);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.1);
}

.about-hero__image {
  width: 100%;
  height: 100%;
  min-height: 260px;
  object-fit: cover;
  display: block;
}

.card-grid,
.visual-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 1rem;
}

.info-card,
.visual-card {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: 18px;
  padding: 1rem;
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.06);
}

.info-card h3,
.visual-card h3 {
  margin: 0;
  color: var(--color-forest);
}

.info-card p,
.visual-card p {
  margin: 0.45rem 0 0;
  color: var(--color-muted);
  line-height: 1.55;
}

.card-meta {
  margin: 0;
  font-size: 0.85rem;
  color: var(--color-rose);
  font-weight: 700;
}

.visual-card {
  padding: 0;
  overflow: hidden;
}

.visual-card img {
  width: 100%;
  min-height: 220px;
  object-fit: cover;
  display: block;
}

.visual-card figcaption {
  padding: 1rem;
}

.section--cta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  background: linear-gradient(135deg, rgba(47, 52, 57, 0.08), rgba(11, 122, 92, 0.12));
  border-radius: 24px;
}

@media (max-width: 900px) {
  .about-hero {
    grid-template-columns: 1fr;
  }

  .section--cta {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
