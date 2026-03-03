<script setup lang="ts">
import { computed, nextTick, onBeforeUnmount, onMounted, ref, watch } from 'vue'

type HeroVideoSource = {
  src: string
  type: string
}

type HeroVideo = {
  sources: HeroVideoSource[]
  poster?: string
}

type Accolade = {
  label: string
  detail: string
}

const heroVideos: HeroVideo[] = [
  {
    sources: [{ src: '/videos/video1.mp4', type: 'video/mp4' }]
  },
  {
    sources: [{ src: '/videos/video2.mp4', type: 'video/mp4' }]
  }
]


const currentVideoIndex = ref(0)
const heroVideoElement = ref<HTMLVideoElement | null>(null)
const scrollOffset = ref(0)
const activeHeroVideo = computed(() => heroVideos[currentVideoIndex.value] ?? heroVideos[0])
const orbitDrift = computed(() => Math.min(scrollOffset.value * 0.08, 80))
const heroFlow = computed(() => Math.min(scrollOffset.value * 0.18, 160))

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

onMounted(() => {
  handleScroll()
  window.addEventListener('scroll', handleScroll, { passive: true })
  heroVideoElement.value?.play().catch(() => {})
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll)
})

watch(currentVideoIndex, async () => {
  await nextTick()
  heroVideoElement.value?.play().catch(() => {})
})
</script>

<template>
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
      <div class="hero__badge">
        <span class="hero__gold">Bahndienstleistungen</span>
      </div>
      <p class="hero__title">Babylon Bahndienste</p>
      <p class="hero__lead">
        Babylon Bahndienste liefert zuverlässige Bahndienstleistungen aus einer Hand – mit eingespielten Teams, klaren Abläufen und kompromisslosen Sicherheitsstandards. Termintreu, sauber dokumentiert, sicher umgesetzt.
      </p>

      <div class="hero__actions">
        <NuxtLink to="/leistungen" class="cta cta--ghost">Leistungen ansehen</NuxtLink>
        <NuxtLink to="/kontakt" class="cta cta--contact">Kontakt aufnehmen</NuxtLink>
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
</template>

<style scoped>
.hero {
  --hero-overlap: 0rem;
  position: relative;
  overflow: hidden;
  border-radius: 0;
  padding: calc(1.2rem + var(--hero-overlap)) clamp(2rem, 4vw, 3rem) 3.6rem;
  background: var(--color-forest);
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.22), inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  min-height: max(540px, calc(100svh - 88px));
  display: grid;
  grid-template-columns: minmax(0, 760px);
  align-items: center;
  justify-content: center;
  column-gap: clamp(1.5rem, 5vw, 3.5rem);
  width: 100vw;
  max-width: none;
  margin-left: calc(-50vw + 50%);
  margin-right: calc(-50vw + 50%);
  margin-top: 0;
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
  filter: saturate(1.05) contrast(1.05) brightness(0.96);
  transform: scale(1.015);
  opacity: 0.94;
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
    linear-gradient(160deg, rgba(0, 72, 49, 0.72), rgba(0, 72, 49, 0.58)),
    radial-gradient(circle at 32% 30%, rgba(199, 117, 139, 0.2), transparent 34%),
    radial-gradient(circle at 72% 65%, rgba(255, 255, 255, 0.12), transparent 40%);
  backdrop-filter: blur(6px);
  mix-blend-mode: normal;
  opacity: 1;
}

.hero__content {
  position: relative;
  z-index: 1;
  max-width: 720px;
  width: min(100%, 720px);
  display: grid;
  gap: 1.1rem;
  color: #ffffff;
  padding: 1.4rem 1.6rem;
  grid-column: 1;
  justify-self: center;
  align-self: center;
  text-align: center;
}

.hero__title {
  margin: 0;
  font-size: clamp(3.3rem, 8vw, 6rem);
  font-weight: 900;
  letter-spacing: -0.03em;
  text-transform: uppercase;
  color: #c7758b;
  text-shadow: 0 18px 36px rgba(0, 0, 0, 0.6);
}

.hero__badge {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.45rem 0.85rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.08);
  color: #ffffff;
  font-size: 0.9rem;
  letter-spacing: 0.04em;
  box-shadow: 0 12px 35px rgba(0, 0, 0, 0.22), inset 0 0 0 1px rgba(255, 255, 255, 0.12);
  width: fit-content;
  justify-self: center;
}

.hero__gold {
  display: inline-block;
  margin-left: 0.35rem;
  color: #ffffff;
  filter: drop-shadow(0 12px 24px rgba(199, 117, 139, 0.35));
}

.hero__lead {
  margin: 0;
  max-width: 640px;
  color: rgba(255, 255, 255, 0.92);
  font-size: 1.08rem;
  line-height: 1.6;
  text-shadow: 0 14px 30px rgba(0, 0, 0, 0.4);
}

.hero__actions {
  display: flex;
  gap: 0.8rem;
  flex-wrap: wrap;
  justify-content: center;
}

.hero :global(.cta--ghost) {
  background: var(--color-rose);
  color: #ffffff;
  border-color: rgba(255, 255, 255, 0.24);
  box-shadow: 0 18px 45px rgba(199, 117, 139, 0.32), inset 0 1px 0 rgba(255, 255, 255, 0.22);
}

.hero :global(.cta--ghost:hover),
.hero :global(.cta--ghost:focus-visible) {
  background: #b8687d;
  transform: translateY(-1px);
  box-shadow: 0 22px 60px rgba(199, 117, 139, 0.38);
}

.hero :global(.cta--contact) {
  background: #005f46;
  color: #ffffff;
  border-color: rgba(255, 255, 255, 0.28);
  box-shadow: 0 18px 45px rgba(0, 95, 70, 0.35), inset 0 1px 0 rgba(255, 255, 255, 0.22);
}

.hero :global(.cta--contact:hover),
.hero :global(.cta--contact:focus-visible) {
  background: #004f3a;
  transform: translateY(-1px);
  box-shadow: 0 22px 60px rgba(0, 95, 70, 0.42);
}

.hero__accolades {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 220px), 1fr));
  gap: 0.9rem;
  margin-top: 0.5rem;
  text-align: left;
}

.hero__accolade {
  padding: 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.04), 0 12px 30px rgba(0, 0, 0, 0.25);
}

.hero__accolade p {
  margin: 0.35rem 0 0;
  color: #d9d9d9;
  font-size: 0.97rem;
  line-height: 1.5;
}

.hero__chip {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.4rem 0.65rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.06);
  color: #ffffff;
  font-size: 0.85rem;
  letter-spacing: 0.03em;
}

.hero__orbit {
  position: absolute;
  border-radius: 50%;
  filter: blur(40px);
  opacity: 0.45;
}

.hero__orbit--one {
  width: 380px;
  height: 380px;
  background: radial-gradient(circle, rgba(199, 117, 139, 0.3), transparent 60%);
  bottom: -80px;
  right: 14%;
}

.hero__orbit--two {
  width: 260px;
  height: 260px;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.14), transparent 60%);
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
    radial-gradient(circle at 50% 30%, rgba(199, 117, 139, 0.2), transparent 38%),
    radial-gradient(circle at 40% 80%, rgba(255, 255, 255, 0.12), transparent 45%),
    conic-gradient(from 140deg at 50% 50%, rgba(0, 72, 49, 0.2), transparent 60%);
  filter: blur(48px) saturate(1.05);
  opacity: 0.65;
  transition: transform 0.35s ease-out;
  pointer-events: none;
}

@media (max-width: 1100px) {
  .hero {
    grid-template-columns: 1fr;
    justify-content: stretch;
    padding: calc(1.4rem + var(--hero-overlap)) clamp(1.4rem, 3vw, 2.4rem) 3.6rem;
  }

  .hero__content {
    grid-column: 1;
    justify-self: center;
    width: 100%;
  }
}

@media (max-width: 700px) {
  .hero {
    min-height: auto;
    padding: 2.4rem 1.2rem 2.6rem;
  }

  .hero__content {
    transform: none;
    padding: 0.8rem 0.2rem;
  }

  .hero__title {
    font-size: clamp(2rem, 11vw, 3.1rem);
  }

  .hero__lead {
    font-size: 1rem;
  }

  .hero__actions {
    width: 100%;
    align-items: center;
  }

  .hero :global(.cta) {
    width: min(80%, 14rem);
    justify-content: center;
    padding: 0.72rem 1rem;
    font-size: 0.95rem;
    border-radius: 10px;
  }

  .hero__orbit--one {
    width: 260px;
    height: 260px;
    right: -20%;
  }

  .hero__orbit--two {
    width: 180px;
    height: 180px;
    left: -12%;
  }
}

@media (max-width: 420px) {
  .hero {
    padding: 2rem 0.9rem 2.2rem;
  }

  .hero__badge {
    font-size: 0.78rem;
  }

  .hero :global(.cta) {
    width: min(78%, 13.5rem);
    padding: 0.68rem 0.9rem;
    font-size: 0.9rem;
  }

  .hero__chip {
    font-size: 0.78rem;
  }
}
</style>
