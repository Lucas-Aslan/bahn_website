<script setup lang="ts">
import { computed, nextTick, onBeforeUnmount, onMounted, ref, watch } from 'vue'


type HeroVideoSource = {
  src: string
  type: string
}

type HeroVideo = {
  sources: HeroVideoSource[]
}

type Accolade = {
  label: string
  detail: string
}

type Metric = {
  value: string
  label: string
}

type Service = {
  accent: string
  title: string
  description: string
}

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

const heroVideos: HeroVideo[] = [
  {
    sources: [
      { src: '/videos/video1.mp4', type: 'video/mp4' },
    ]
  },
  {
    sources: [
      { src: '/videos/video2.mp4', type: 'video/mp4' },
    ]
  }
]

const currentVideoIndex = ref(0)
const heroVideoElement = ref<HTMLVideoElement | null>(null)
const scrollOffset = ref(0)
let revealObserver: IntersectionObserver | null = null

const activeHeroVideo = computed(() => heroVideos[currentVideoIndex.value] ?? heroVideos[0])

const handleScroll = () => {
  scrollOffset.value = window.scrollY
}

const handleHeroVideoEnded = async () => {
  if (heroVideos.length <= 1) {
    await heroVideoElement.value?.play().catch(() => {})
    return
  }
  currentVideoIndex.value = (currentVideoIndex.value + 1) % heroVideos.length
}

const orbitDrift = computed(() => Math.min(scrollOffset.value * 0.08, 80))

const heroFlow = computed(() => Math.min(scrollOffset.value * 0.18, 160))

onMounted(() => {
  handleScroll()
  window.addEventListener('scroll', handleScroll, { passive: true })

  heroVideoElement.value?.play().catch(() => {})

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
    element.style.setProperty('--reveal-delay', `${index * 80}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll)
  revealObserver?.disconnect()
})

watch(currentVideoIndex, async () => {
  await nextTick()
  heroVideoElement.value?.play().catch(() => {})
})
</script>

<template>
  <div class="page">
    <section class="hero">
      <div class="hero__video" aria-hidden="true">
        <Transition name="hero-video" mode="out-in">
          <video
            :key="activeHeroVideo.sources[0]?.src"
            ref="heroVideoElement"
            autoplay
            muted
            :loop="heroVideos.length === 1"
            playsinline
            :poster="activeHeroVideo.poster"
            @ended="handleHeroVideoEnded"
          >
            <source
              v-for="source in activeHeroVideo.sources"
              :key="source.src"
              :src="source.src"
              :type="source.type"
            >
          </video>
        </Transition>
        <div class="hero__tint" />
      </div>

      <div class="hero__content">
        <div class="hero__badge"> <span class="hero__gold">Bahndienstleistungen</span></div>
        <p class="hero__title">Babylon Bahndienste</p>
        <p class="hero__lead">
          Babylon Bahndienste unterstützt Projekte rund um die Schiene mit erfahrenen Teams, strukturierten Abläufen und
          höchsten Sicherheitsstandards – termintreu und präzise umgesetzt.
        </p>

        <div class="hero__actions">
          <NuxtLink to="/kontakt" class="cta cta--solid">Projekt anfragen</NuxtLink>
          <NuxtLink to="/leistungen/transport" class="cta cta--ghost">Leistungen ansehen</NuxtLink>
        </div>

        <div class="hero__accolades" role="list">
          <div
            v-for="item in accolades"
            :key="item.label"
            class="hero__accolade"
            role="listitem"
          >
            <span class="hero__chip">{{ item.label }}</span>
            <p>{{ item.detail }}</p>
          </div>
        </div>
      </div>

      <div
        class="hero__orbit hero__orbit--one"
        aria-hidden="true"
        :style="{ transform: `translateY(${orbitDrift * 0.6}px) rotate(${orbitDrift / 2}deg)` }"
      />
      <div
        class="hero__orbit hero__orbit--two"
        aria-hidden="true"
        :style="{ transform: `translateY(${orbitDrift * -0.4}px) rotate(${orbitDrift / -3}deg)` }"
      />
      <div
        class="hero__flow"
        aria-hidden="true"
        :style="{ transform: `translate(-50%, ${heroFlow}px)` }"
      />
    </section>

    <section id="about" class="about section js-reveal">
      <div class="about__entry-overlay" aria-hidden="true">
        <span class="about__beam about__beam--left" />
        <span class="about__beam about__beam--center" />
        <span class="about__beam about__beam--right" />
      </div>
      <div class="about__inner">
        <div class="about__header">
          <div class="about__eyebrow">
            <p class="eyebrow">Über uns</p>
            <span class="about__spark" aria-hidden="true" />
          </div>
          <h2>Präzision, Sicherheit, partnerschaftlich.</h2>
          <p class="section__lead">
            Babylon Bahndienste ist Ihr zuverlässiger Partner rund um die Schiene: erfahrene Teams, klare Abläufe und
            konsequente Sicherheit – von der Planung bis zum Einsatz vor Ort. Transparente Kommunikation und saubere
            Dokumentation halten Projekte planbar und den Bahnbetrieb stabil.
          </p>

          <div class="about__highlights" role="list">
            <div class="about__highlight" role="listitem">
              <span class="about__pulse" aria-hidden="true" />
              <div>
                <p class="about__label">Einsatzsicherheit</p>
                <p class="about__description">Sicherungslogik, Unterweisungen und Reporting bleiben lückenlos.</p>
              </div>
            </div>
            <div class="about__highlight" role="listitem">
              <span class="about__pulse about__pulse--gold" aria-hidden="true" />
              <div>
                <p class="about__label">Planung bis Umsetzung</p>
                <p class="about__description">Von der Crew-Dispo bis zum Vor-Ort-Einsatz alles aus einer Hand.</p>
              </div>
            </div>
            <div class="about__highlight" role="listitem">
              <span class="about__pulse about__pulse--cyan" aria-hidden="true" />
              <div>
                <p class="about__label">Partnerschaftlich</p>
                <p class="about__description">Transparente Kommunikation und proaktive Abstimmung mit Auftraggebern.</p>
              </div>
            </div>
          </div>

          <div class="about__actions">
            <NuxtLink to="/about" class="about__cta about__cta--solid">
              Mehr über uns
              <span aria-hidden="true">→</span>
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

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
          :style="{ '--card-delay': `${index * 100}ms` }"
        >
          <div class="performance-card__header">
            <span class="performance-card__badge">{{ block.badge }}</span>
            <h3>{{ block.title }}</h3>
            <p class="performance-card__summary">{{ block.summary }}</p>
          </div>
          <ul class="performance-card__list">
            <li v-for="point in block.points" :key="point" class="performance-card__item">
              <span class="performance-card__icon" aria-hidden="true">✦</span>
              <span>{{ point }}</span>
            </li>
          </ul>
          <div class="performance-card__glow" aria-hidden="true" />
        </article>
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header">
        <div class="metrics" role="list">
          <div
            v-for="metric in metrics"
            :key="metric.label"
            class="metric"
            role="listitem"
          >
            <span class="metric__value">{{ metric.value }}</span>
            <span class="metric__label">{{ metric.label }}</span>
          </div>
        </div>
      </div>

      <div class="service-grid">
        <article
          v-for="service in services"
          :key="service.title"
          class="service-card js-reveal"
        >
          <span class="service-card__accent">{{ service.accent }}</span>
          <h3>{{ service.title }}</h3>
          <p>{{ service.description }}</p>
          <div class="service-card__glow" aria-hidden="true" />
        </article>
      </div>
    </section>
  </div>
</template>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.hero {
  --hero-overlap: clamp(4.5rem, 12vh, 6.5rem);
  --hero-bleed: calc(var(--hero-overlap) + 1.25rem);
  position: relative;
  overflow: hidden;
  border-radius: 0;
  padding: calc(3.5rem + var(--hero-bleed)) clamp(1.4rem, 3vw, 2.4rem) 3.8rem;
  background: linear-gradient(135deg, rgba(9, 12, 24, 0.92), rgba(5, 11, 24, 0.7));
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.55), inset 0 0 0 1px rgba(255, 255, 255, 0.04);
  min-height: 540px;
  display: grid;
  align-items: center;
  width: 100vw;
  max-width: none;
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  margin-top: calc(-1rem - var(--hero-bleed));
}

.hero__video {
  position: absolute;
  inset: 0;
  z-index: 0;
  overflow: hidden;
}

.hero__video video {
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: saturate(1.05) contrast(1.12) brightness(0.92);
  transform: scale(1.015);
  opacity: 0.98;
}

.hero-video-enter-active,
.hero-video-leave-active {
  transition: opacity 0.9s ease, transform 1.2s ease;
}

.hero-video-enter-from,
.hero-video-leave-to {
  opacity: 0;
  transform: scale(1.04);
}

.hero__tint {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(circle at 32% 30%, rgba(255, 185, 80, 0.22), transparent 34%),
    linear-gradient(130deg, rgba(6, 12, 24, 0.2), rgba(0, 0, 0, 0.55) 55%, rgba(4, 12, 25, 0.78));
  backdrop-filter: blur(2px);
  mix-blend-mode: multiply;
  opacity: 0.94;
}

.hero__nameplate {
  position: absolute;
  inset: 12% auto auto 8%;
  font-size: clamp(3rem, 8vw, 6rem);
  font-weight: 800;
  letter-spacing: -0.03em;
  text-transform: uppercase;
  color: #f9d270;
  opacity: 0.12;
  filter: drop-shadow(0 28px 60px rgba(249, 210, 112, 0.18));
  transform: translateY(var(--nameplate-shift, 0));
  transition: transform 0.2s ease-out;
  pointer-events: none;
}

.hero__content {
  position: relative;
  z-index: 1;
  max-width: 720px;
  display: grid;
  gap: 1.1rem;
  color: #e8f0ff;
  padding: 1.4rem 1.6rem;
  border-radius: 18px;
  background: linear-gradient(135deg, rgba(7, 12, 22, 0.78), rgba(5, 10, 20, 0.64));
  backdrop-filter: blur(9px) saturate(1.05);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 28px 80px rgba(0, 0, 0, 0.38), inset 0 1px 0 rgba(255, 255, 255, 0.05);
}

.hero__title {
  margin: 0;
  font-size: clamp(2.8rem, 6vw, 4.8rem);
  font-weight: 900;
  letter-spacing: -0.03em;
  text-transform: uppercase;
  background: linear-gradient(115deg, #f6e6b4, #f9d270 40%, #c99038);
  -webkit-background-clip: text;
  color: transparent;
  filter: drop-shadow(0 12px 28px rgba(249, 210, 112, 0.28));
}

.hero__badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.45rem 0.85rem;
  border-radius: 999px;
  background: linear-gradient(120deg, rgba(255, 205, 120, 0.18), rgba(255, 255, 255, 0.08));
  color: #f8dba1;
  font-size: 0.9rem;
  letter-spacing: 0.04em;
  box-shadow: 0 15px 45px rgba(0, 0, 0, 0.3), inset 0 0 0 1px rgba(255, 214, 138, 0.2);
  width: fit-content;
}

h1 {
  margin: 0;
  font-size: clamp(2.6rem, 4vw, 3.6rem);
  line-height: 1.05;
  letter-spacing: -0.015em;
  text-shadow: 0 20px 60px rgba(0, 0, 0, 0.55);
}

.hero__gold {
  display: inline-block;
  margin-left: 0.35rem;
  background: linear-gradient(120deg, #f6e6b4, #f9d270 45%, #c99038);
  -webkit-background-clip: text;
  color: transparent;
  filter: drop-shadow(0 12px 28px rgba(249, 210, 112, 0.2));
}

.hero__lead {
  margin: 0;
  max-width: 640px;
  color: #cfe2ff;
  font-size: 1.08rem;
  line-height: 1.6;
  text-shadow: 0 14px 30px rgba(0, 0, 0, 0.55);
}

.hero__actions {
  display: flex;
  gap: 0.8rem;
  flex-wrap: wrap;
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
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease, border-color 0.2s ease;
  border: 1px solid transparent;
}

.cta--solid {
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  box-shadow: 0 18px 45px rgba(249, 210, 112, 0.35), inset 0 1px 0 rgba(255, 255, 255, 0.3);
}

.cta--solid:hover,
.cta--solid:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 60px rgba(249, 210, 112, 0.45);
}

.cta--ghost {
  background: rgba(255, 255, 255, 0.04);
  color: #f6e6b4;
  border-color: rgba(255, 226, 153, 0.3);
  backdrop-filter: blur(8px);
}

.cta--ghost:hover,
.cta--ghost:focus-visible {
  transform: translateY(-1px);
  background: rgba(255, 255, 255, 0.08);
}

.hero__accolades {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 0.9rem;
  margin-top: 0.5rem;
}

.hero__accolade {
  padding: 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.02);
}

.hero__accolade p {
  margin: 0.35rem 0 0;
  color: #d9e7ff;
  font-size: 0.97rem;
  line-height: 1.5;
}

.hero__chip {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.4rem 0.65rem;
  border-radius: 999px;
  background: rgba(249, 210, 112, 0.15);
  color: #f9d270;
  font-size: 0.85rem;
  letter-spacing: 0.03em;
}

.hero__orbit {
  position: absolute;
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0.6;
}

.hero__orbit--one {
  width: 380px;
  height: 380px;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.28), transparent 60%);
  bottom: -80px;
  right: 14%;
}

.hero__orbit--two {
  width: 260px;
  height: 260px;
  background: radial-gradient(circle, rgba(0, 255, 255, 0.18), transparent 60%);
  top: -60px;
  left: 10%;
}

.hero__flow {
  position: absolute;
  left: 50%;
  bottom: -40%;
  width: 620px;
  height: 620px;
  background:
    radial-gradient(circle at 50% 30%, rgba(249, 210, 112, 0.16), transparent 38%),
    radial-gradient(circle at 40% 80%, rgba(0, 255, 255, 0.14), transparent 45%),
    conic-gradient(from 140deg at 50% 50%, rgba(249, 210, 112, 0.14), transparent 60%);
  filter: blur(48px) saturate(1.1);
  opacity: 0.7;
  transition: transform 0.35s ease-out;
  pointer-events: none;
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

.section {
  background: rgba(6, 12, 26, 0.8);
  border-radius: 24px;
  padding: clamp(1.5rem, 2vw, 2rem);
  border: 1px solid rgba(255, 255, 255, 0.05);
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.4);
}

.about {
  position: relative;
  overflow: hidden;
  padding: clamp(2rem, 3vw, 2.8rem);
  background:
    linear-gradient(135deg, #f8d770, #e8b94f),
    radial-gradient(circle at 14% 20%, rgba(255, 255, 255, 0.28), transparent 40%),
    radial-gradient(circle at 82% 72%, rgba(233, 175, 60, 0.32), transparent 36%);
  border: 1px solid rgba(131, 87, 8, 0.24);
  box-shadow: 0 30px 80px rgba(115, 78, 5, 0.32);
  color: #2a1a04;
  transform-style: preserve-3d;
  transform-origin: center center;
  transition:
    transform 0.9s cubic-bezier(0.2, 0.7, 0.15, 1),
    opacity 0.9s ease,
    filter 0.9s ease,
    box-shadow 0.9s ease;
}

.about h2 {
  color: #1c1403;
}

.about .section__lead {
  color: #4a3200;
}

.about__inner {
  display: grid;
  gap: 2.4rem;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  align-items: start;
  position: relative;
}

.about__inner::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 28%, rgba(255, 244, 214, 0.25), transparent 36%),
    radial-gradient(circle at 82% 62%, rgba(233, 175, 60, 0.2), transparent 32%);
  pointer-events: none;
  z-index: 0;
}

.about__header {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 1rem;
}

.about__entry-overlay {
  position: absolute;
  inset: -10%;
  pointer-events: none;
  overflow: hidden;
  z-index: 0;
  opacity: 0;
}

.about__beam {
  position: absolute;
  inset: 0;
  background: linear-gradient(105deg, rgba(255, 255, 255, 0.24), rgba(255, 255, 255, 0));
  filter: blur(24px);
  transform: translateY(32px) skewX(-12deg) scaleX(0.6);
  mix-blend-mode: screen;
  border-radius: 18px;
  opacity: 0.65;
}

.about__beam--left {
  left: -26%;
  width: 40%;
}

.about__beam--center {
  left: 10%;
  width: 38%;
  filter: blur(30px);
  opacity: 0.5;
}

.about__beam--right {
  right: -24%;
  width: 42%;
  filter: blur(22px);
  opacity: 0.7;
}

.about.js-reveal {
  transform: translateY(28px) scale(0.985) rotateX(5deg);
  filter: blur(8px) saturate(0.9);
}

.about.js-reveal.is-visible {
  transform: translateY(0) scale(1) rotateX(0deg);
  filter: blur(0) saturate(1.05);
  box-shadow: 0 35px 90px rgba(115, 78, 5, 0.38), 0 0 0 1px rgba(255, 255, 255, 0.05);
}

.about.js-reveal.is-visible .about__entry-overlay {
  opacity: 1;
  animation: curtainSweep 1.2s cubic-bezier(0.17, 0.86, 0.25, 1) forwards;
}

.about.js-reveal.is-visible .about__beam--left {
  animation: beamSlide 1.2s 0.05s cubic-bezier(0.2, 0.8, 0.1, 1) forwards;
}

.about.js-reveal.is-visible .about__beam--center {
  animation: beamSlide 1.2s 0.12s cubic-bezier(0.2, 0.8, 0.1, 1) forwards;
}

.about.js-reveal.is-visible .about__beam--right {
  animation: beamSlide 1.2s 0.18s cubic-bezier(0.2, 0.8, 0.1, 1) forwards;
}

.about.js-reveal.is-visible .about__header,
.about.js-reveal.is-visible .about__highlights,
.about.js-reveal.is-visible .about__actions {
  animation: contentLift 0.8s 0.1s ease forwards;
}

.about__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
}

@keyframes curtainSweep {
  0% {
    clip-path: inset(0 0 0 0);
    opacity: 0.9;
    transform: translateY(32px);
  }
  60% {
    clip-path: inset(0 0 0 55%);
    opacity: 0.75;
    transform: translateY(6px);
  }
  100% {
    clip-path: inset(0 0 0 100%);
    opacity: 0;
    transform: translateY(-10px);
  }
}

@keyframes beamSlide {
  from {
    transform: translateY(28px) skewX(-12deg) scaleX(0.6);
    opacity: 0;
  }
  40% {
    opacity: 0.7;
  }
  to {
    transform: translateY(-38px) skewX(-8deg) scaleX(1.05);
    opacity: 0;
  }
}

@keyframes contentLift {
  from {
    transform: translateY(18px);
    opacity: 0;
  }
  65% {
    transform: translateY(-4px);
    opacity: 1;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

.about .eyebrow {
  color: #734703;
}

.about__spark {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: radial-gradient(circle, #f9d270 0%, rgba(249, 210, 112, 0.4) 70%, transparent 100%);
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.5);
  animation: pulse 2.2s ease-in-out infinite;
}

.about__cta {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-weight: 700;
  color: #3b2400;
  text-decoration: none;
  margin-top: 0.2rem;
  padding: 0.65rem 1rem;
  border-radius: 12px;
  border: 1px solid rgba(99, 64, 2, 0.16);
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease, background 0.2s ease;
  backdrop-filter: blur(6px);
}

.about__cta:hover,
.about__cta:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 12px 30px rgba(99, 64, 2, 0.18);
  border-color: rgba(99, 64, 2, 0.36);
  background: rgba(255, 255, 255, 0.18);
  text-decoration: none;
}

.about__cta--solid {
  background: linear-gradient(135deg, #0c0a05, #151008);
  color: #f6c54c;
  border: 1px solid rgba(246, 197, 76, 0.4);
}

.about__cta--solid:hover,
.about__cta--solid:focus-visible {
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.25), 0 0 0 1px rgba(246, 197, 76, 0.32);
  transform: translateY(-2px) scale(1.01);
}

.about__cta--ghost {
  color: #eaf2ff;
  border-color: rgba(255, 255, 255, 0.18);
  background: rgba(255, 255, 255, 0.02);
}

.about__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.about__highlights {
  display: grid;
  gap: 0.7rem;
  margin: 0.4rem 0 0.8rem;
}

.about__highlight {
  display: grid;
  gap: 0.1rem;
  grid-template-columns: auto 1fr;
  align-items: start;
  padding: 0.7rem 0.8rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.74);
  border: 1px solid rgba(122, 83, 8, 0.2);
  box-shadow: 0 12px 30px rgba(122, 83, 8, 0.18);
}

.about__pulse {
  margin-top: 0.12rem;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(0, 0, 0, 0.9), rgba(0, 0, 0, 0));
  box-shadow: 0 0 0 0 rgba(0, 0, 0, 0.48);
  animation: pulse 1.9s ease-in-out infinite;
}

.about__pulse--gold {
  background: radial-gradient(circle, rgba(12, 8, 3, 0.9), rgba(12, 8, 3, 0));
  box-shadow: 0 0 0 0 rgba(12, 8, 3, 0.56);
}

.about__pulse--cyan {
  background: radial-gradient(circle, rgba(18, 13, 6, 0.9), rgba(18, 13, 6, 0));
  box-shadow: 0 0 0 0 rgba(18, 13, 6, 0.52);
}

.about__label {
  margin: 0;
  font-weight: 700;
  letter-spacing: 0.01em;
  color: #241503;
}

.about__description {
  margin: 0.08rem 0 0;
  color: #4a3200;
  line-height: 1.5;
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 currentColor;
    transform: scale(1);
  }
  60% {
    box-shadow: 0 0 0 10px transparent;
    transform: scale(1.06);
  }
  100% {
    box-shadow: 0 0 0 0 transparent;
    transform: scale(1);
  }
}

.section__header {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.4rem;
  align-items: end;
}

.eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: #8ec5ff;
  font-size: 0.82rem;
}

.section h2 {
  margin: 0.2rem 0 0.35rem;
  font-size: clamp(1.8rem, 3vw, 2.3rem);
  letter-spacing: -0.01em;
}

.section__lead {
  margin: 0;
  color: #c8dbff;
  line-height: 1.6;
}

.metrics {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
  gap: 0.8rem;
}

.performance {
  background: radial-gradient(circle at 18% 24%, rgba(249, 210, 112, 0.06), transparent 36%),
    radial-gradient(circle at 82% 68%, rgba(201, 144, 56, 0.08), transparent 32%),
    linear-gradient(135deg, #090909, #050505);
  border: 1px solid rgba(249, 210, 112, 0.18);
  box-shadow: 0 28px 75px rgba(0, 0, 0, 0.6), inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  color: #f6e6b4;
}

.performance__lead {
  color: #e0c78a;
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
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  text-decoration: none;
  font-weight: 800;
  letter-spacing: 0.02em;
  box-shadow: 0 18px 45px rgba(249, 210, 112, 0.25);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.performance__cta:hover,
.performance__cta:focus-visible {
  transform: translateY(-2px);
  box-shadow: 0 24px 60px rgba(249, 210, 112, 0.3);
}

.performance__grid {
  margin-top: 1.4rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem;
}

.performance-card {
  position: relative;
  overflow: hidden;
  padding: 1.1rem 1.1rem 1rem;
  border-radius: 18px;
  background: linear-gradient(145deg, rgba(12, 12, 14, 0.95), rgba(6, 6, 8, 0.95));
  border: 1px solid rgba(249, 210, 112, 0.18);
  box-shadow: 0 18px 50px rgba(0, 0, 0, 0.55), inset 0 1px 0 rgba(255, 255, 255, 0.04);
  color: #f6e6b4;
  transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
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
  transform: translateY(-6px);
  border-color: rgba(249, 210, 112, 0.34);
  box-shadow: 0 26px 65px rgba(0, 0, 0, 0.65), 0 0 0 1px rgba(249, 210, 112, 0.18);
}

.performance-card__header {
  display: grid;
  gap: 0.35rem;
}

.performance-card__badge {
  width: fit-content;
  padding: 0.28rem 0.65rem;
  border-radius: 999px;
  background: rgba(249, 210, 112, 0.18);
  color: #f9d270;
  letter-spacing: 0.08em;
  font-size: 0.78rem;
  text-transform: uppercase;
  border: 1px solid rgba(249, 210, 112, 0.2);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08);
}

.performance-card h3 {
  margin: 0;
  font-size: 1.22rem;
  letter-spacing: -0.01em;
}

.performance-card__summary {
  margin: 0;
  color: #e8d59f;
  line-height: 1.5;
}

.performance-card__list {
  margin: 0.7rem 0 0;
  padding: 0;
  list-style: none;
  display: grid;
  gap: 0.45rem;
}

.performance-card__item {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: start;
  gap: 0.5rem;
  color: #fdf2c7;
  font-weight: 600;
}

.performance-card__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.35), rgba(249, 210, 112, 0));
  border: 1px solid rgba(249, 210, 112, 0.24);
  color: #f9d270;
  font-size: 0.85rem;
  box-shadow: 0 10px 22px rgba(0, 0, 0, 0.4), inset 0 1px 0 rgba(255, 255, 255, 0.06);
}

.performance-card__glow {
  position: absolute;
  inset: -12%;
  background: radial-gradient(circle at 24% 24%, rgba(249, 210, 112, 0.12), transparent 38%),
    radial-gradient(circle at 78% 70%, rgba(201, 144, 56, 0.1), transparent 40%);
  opacity: 0.65;
  pointer-events: none;
  animation: performanceGlow 6s ease-in-out infinite;
}

.performance-card::after {
  content: '';
  position: absolute;
  inset: 1px;
  border-radius: 17px;
  background: linear-gradient(120deg, rgba(249, 210, 112, 0.12), rgba(249, 210, 112, 0));
  opacity: 0.8;
  mix-blend-mode: screen;
  pointer-events: none;
  filter: blur(1px);
}

.performance-card:hover::after,
.performance-card:focus-within::after {
  opacity: 1;
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

.metric {
  padding: 0.9rem 1rem;
  border-radius: 16px;
  background: linear-gradient(135deg, rgba(0, 255, 255, 0.12), rgba(255, 255, 255, 0.02));
  border: 1px solid rgba(255, 255, 255, 0.05);
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.35);
  display: grid;
  gap: 0.18rem;
}

.metric__value {
  font-size: 1.3rem;
  font-weight: 800;
  color: #f9d270;
}

.metric__label {
  color: #d6e6ff;
  font-size: 0.95rem;
  line-height: 1.4;
}

.service-grid {
  margin-top: 1.5rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.service-card {
  position: relative;
  overflow: hidden;
  padding: 1.4rem 1.2rem;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.05);
  min-height: 180px;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.35);
  transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
}

.service-card:hover,
.service-card:focus-within {
  transform: translateY(-4px);
  border-color: rgba(249, 210, 112, 0.4);
  box-shadow: 0 24px 60px rgba(249, 210, 112, 0.2);
}

.service-card h3 {
  margin: 0.2rem 0 0.4rem;
  font-size: 1.2rem;
}

.service-card p {
  margin: 0;
  color: #d6e6ff;
  line-height: 1.5;
  font-size: 0.98rem;
}

.service-card__accent {
  display: inline-flex;
  padding: 0.3rem 0.65rem;
  border-radius: 999px;
  background: rgba(0, 255, 255, 0.14);
  color: #74e3ff;
  font-size: 0.85rem;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.service-card__glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 80% 20%, rgba(249, 210, 112, 0.14), transparent 45%),
    radial-gradient(circle at 20% 80%, rgba(0, 255, 255, 0.12), transparent 40%);
  opacity: 0;
  transition: opacity 0.2s ease;
}

.service-card:hover .service-card__glow,
.service-card:focus-within .service-card__glow {
  opacity: 1;
}

@media (max-width: 700px) {
  .hero {
    padding: 2.4rem 1.2rem 2.6rem;
  }

  .hero__lead {
    font-size: 1rem;
  }

  .hero__actions {
    width: 100%;
  }

  .cta {
    width: 100%;
  }

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
