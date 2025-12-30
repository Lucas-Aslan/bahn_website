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
