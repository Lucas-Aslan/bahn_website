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
