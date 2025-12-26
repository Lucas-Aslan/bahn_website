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

type AboutHighlight = {
  title: string
  detail: string
}

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

const accolades: Accolade[] = [
  {
    label: 'Präzision im Gleis',
    detail: 'Eingespielte Teams, die jede Logistik-Aufgabe auf der Schiene taktisch abwickeln.'
  },
  {
    label: 'Sicherheit zuerst',
    detail: 'Zertifizierte Prozesse, vorausschauende Planung und lückenlose Dokumentation.'
  },
  {
    label: 'Echte Partnerschaft',
    detail: 'Wir denken Projekte mit – von der Vorbereitung bis zum letzten Signal.'
  }
]

const metrics: Metric[] = [
  { value: '24/7', label: 'Einsatzbereit mit Crew & Gerät' },
  { value: '98%', label: 'Termintreue bei Projektübergaben' },
  { value: '12+', label: 'Großprojekte in Deutschland betreut' }
]

const services: Service[] = [
  {
    accent: 'Transport',
    title: 'Präzisions-Transport',
    description: 'Spezialisierte Transporte für Bahnanlagen, Materialien und sensible Komponenten.'
  },
  {
    accent: 'Bau',
    title: 'Infrastruktur-Bau',
    description: 'Koordination, Aufbau und Sicherung von Gleis- und Anlagenprojekten.'
  },
  {
    accent: 'Logistik',
    title: 'Terminal & Logistik',
    description: 'Steuerung von Materialflüssen, Umschlag und Lagerung entlang der Schiene.'
  }
]

const aboutHighlights: AboutHighlight[] = [
  {
    title: 'Crew mit Bahnerfahrung',
    detail: 'Lokführer, Sicherungsposten und Dispo arbeiten als ein Team – klar geführt und briefingstark.'
  },
  {
    title: 'Planbar & transparent',
    detail: 'Dashboards, Check-ins und kurze Feedback-Loops halten alle Beteiligten im Takt.'
  },
  {
    title: 'Einsatzbereit in Stunden',
    detail: 'Wir aktivieren Material und Personal in kürzester Zeit, wenn Projekte Geschwindigkeit brauchen.'
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
        <p class="hero__title">Babylon Bahndienste UG</p>
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
      <div class="about__inner">
        <div class="about__intro">
          <p class="eyebrow">Über uns</p>
          <h2>Teams, die Bahnhöfe und Baustellen in Bewegung halten.</h2>
          <p class="section__lead">
            Wir verbinden Einsatzbereitschaft, Präzision und klare Kommunikation. Mit kurzen Wegen, viel Erfahrung und
            einem Auge fürs Detail begleiten wir Bahnprojekte von der ersten Absprache bis zur fertigen Übergabe.
          </p>
          <div class="about__chips" role="list">
            <span class="about__chip" role="listitem">Operational Excellence</span>
            <span class="about__chip" role="listitem">Sifa-geschult &amp; zertifiziert</span>
            <span class="about__chip" role="listitem">Crew ready on call</span>
          </div>
        </div>

        <div class="about__layout">
          <div class="about__panel js-reveal">
            <div class="about__panel-heading">
              <span class="about__signal" aria-hidden="true"></span>
              <div>
                <p class="about__panel-kicker">Mit jedem Meter abgestimmt</p>
                <p class="about__panel-title">Wir denken Projekte taktisch.</p>
              </div>
            </div>
            <p class="about__panel-copy">
              Jede Schicht beginnt mit Briefing, Safety-Check und einem glasklaren Ablaufplan. So bleiben Züge, Menschen
              und Material sicher im Takt – auch wenn sich die Rahmenbedingungen ändern.
            </p>
            <div class="about__panel-stats" role="list">
              <div class="about__panel-stat" role="listitem">
                <span class="about__panel-value">15 min</span>
                <span class="about__panel-label">Reaktionszeit auf Lageänderungen</span>
              </div>
              <div class="about__panel-stat" role="listitem">
                <span class="about__panel-value">0</span>
                <span class="about__panel-label">Ausfälle bei Sicherheit &amp; QS</span>
              </div>
            </div>
          </div>

          <div class="about__cards">
            <article
              v-for="item in aboutHighlights"
              :key="item.title"
              class="about__card js-reveal"
            >
              <h3>{{ item.title }}</h3>
              <p>{{ item.detail }}</p>
              <span class="about__pulse" aria-hidden="true"></span>
            </article>
          </div>
        </div>
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
  position: relative;
  overflow: hidden;
  border-radius: 26px;
  padding: 3.5rem clamp(1.4rem, 3vw, 2.4rem) 3.8rem;
  background: linear-gradient(135deg, rgba(9, 12, 24, 0.92), rgba(5, 11, 24, 0.7));
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.55), inset 0 0 0 1px rgba(255, 255, 255, 0.04);
  min-height: 540px;
  display: grid;
  align-items: center;
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
  padding: clamp(1.8rem, 3vw, 2.6rem);
  background:
    linear-gradient(145deg, rgba(8, 14, 30, 0.9), rgba(6, 10, 22, 0.92)),
    radial-gradient(circle at 18% 20%, rgba(0, 255, 255, 0.08), transparent 38%),
    radial-gradient(circle at 82% 70%, rgba(249, 210, 112, 0.12), transparent 32%);
  border: 1px solid rgba(255, 255, 255, 0.06);
}

.about__inner {
  display: grid;
  gap: 1.8rem;
}

.about__intro {
  max-width: 820px;
  display: grid;
  gap: 0.65rem;
}

.about__chips {
  display: flex;
  gap: 0.55rem;
  flex-wrap: wrap;
}

.about__chip {
  padding: 0.45rem 0.9rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.18);
  color: #f6e6b4;
  font-weight: 700;
  letter-spacing: 0.02em;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
}

.about__layout {
  display: grid;
  grid-template-columns: minmax(280px, 1fr) minmax(360px, 1.2fr);
  gap: 1.4rem;
  align-items: stretch;
}

.about__panel {
  position: relative;
  padding: 1.4rem 1.3rem;
  border-radius: 18px;
  background: rgba(8, 12, 20, 0.88);
  border: 1px solid rgba(255, 255, 255, 0.04);
  box-shadow: 0 22px 60px rgba(0, 0, 0, 0.42);
  overflow: hidden;
}

.about__panel::after {
  content: '';
  position: absolute;
  inset: -20% -30% auto auto;
  height: 160px;
  width: 220px;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.14), transparent 52%);
  filter: blur(18px);
  opacity: 0.8;
}

.about__panel-heading {
  display: flex;
  align-items: center;
  gap: 0.9rem;
}

.about__panel-kicker {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #8ec5ff;
  font-size: 0.82rem;
}

.about__panel-title {
  margin: 0.1rem 0 0;
  font-size: 1.4rem;
  letter-spacing: -0.015em;
}

.about__panel-copy {
  margin: 1rem 0 1.2rem;
  color: #d6e6ff;
  line-height: 1.6;
}

.about__panel-copy strong {
  color: #f9d270;
}

.about__panel-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
  gap: 0.8rem;
}

.about__panel-stat {
  padding: 0.9rem 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.02);
}

.about__panel-value {
  display: block;
  font-size: 1.2rem;
  font-weight: 800;
  color: #f9d270;
}

.about__panel-label {
  color: #cfe2ff;
  font-size: 0.95rem;
  line-height: 1.4;
}

.about__signal {
  width: 18px;
  height: 18px;
  border-radius: 4px;
  background: linear-gradient(135deg, #f9d270, #c99038);
  box-shadow: 0 0 0 6px rgba(249, 210, 112, 0.16), 0 0 0 12px rgba(249, 210, 112, 0.06), 0 12px 30px rgba(249, 210, 112, 0.4);
  position: relative;
}

.about__signal::after {
  content: '';
  position: absolute;
  inset: -12px;
  border-radius: 10px;
  border: 1px dashed rgba(249, 210, 112, 0.4);
  animation: signal-pulse 2.6s ease-in-out infinite;
}

.about__cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}

.about__card {
  position: relative;
  padding: 1.2rem 1rem 1.4rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  min-height: 160px;
  overflow: hidden;
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.36);
  transition: transform 0.2s ease, border-color 0.2s ease, box-shadow 0.2s ease;
}

.about__card h3 {
  margin: 0 0 0.35rem;
  font-size: 1.08rem;
}

.about__card p {
  margin: 0;
  color: #d6e6ff;
  line-height: 1.5;
}

.about__card:hover,
.about__card:focus-within {
  transform: translateY(-4px);
  border-color: rgba(249, 210, 112, 0.4);
  box-shadow: 0 22px 60px rgba(249, 210, 112, 0.22);
}

.about__pulse {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 18% 28%, rgba(0, 255, 255, 0.12), transparent 36%),
    radial-gradient(circle at 82% 72%, rgba(249, 210, 112, 0.12), transparent 40%);
  opacity: 0;
  transition: opacity 0.25s ease;
}

.about__card:hover .about__pulse,
.about__card:focus-within .about__pulse {
  opacity: 1;
}

@keyframes signal-pulse {
  0% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.6;
  }
  100% {
    transform: scale(1);
    opacity: 1;
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
}
</style>
