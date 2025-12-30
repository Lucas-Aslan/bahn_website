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
        Babylon Bahndienste unterstützt Projekte rund um die Schiene mit erfahrenen Teams, strukturierten Abläufen und
        höchsten Sicherheitsstandards – termintreu und präzise umgesetzt.
      </p>

      <div class="hero__actions">
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
</template>

<style scoped>
.hero {
  --hero-overlap: clamp(4.5rem, 12vh, 6.5rem);
  --hero-bleed: calc(var(--hero-overlap) + 1.25rem);
  position: relative;
  overflow: hidden;
  border-radius: 0;
  padding: calc(1.2rem + var(--hero-overlap)) clamp(2rem, 4vw, 3rem) 3.6rem;
  background: linear-gradient(135deg, rgba(9, 12, 24, 0.92), rgba(5, 11, 24, 0.7));
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.55), inset 0 0 0 1px rgba(255, 255, 255, 0.04);
  min-height: 540px;
  display: grid;
  grid-template-columns: minmax(0, 760px) 1fr;
  align-items: start;
  justify-content: start;
  column-gap: clamp(1.5rem, 5vw, 3.5rem);
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

.hero__content {
  position: relative;
  z-index: 1;
  max-width: 720px;
  width: min(100%, 720px);
  display: grid;
  gap: 1.1rem;
  color: #e8f0ff;
  padding: 1.4rem 1.6rem;
  border-radius: 18px;
  background: linear-gradient(135deg, rgba(7, 12, 22, 0.78), rgba(5, 10, 20, 0.64));
  backdrop-filter: blur(9px) saturate(1.05);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 28px 80px rgba(0, 0, 0, 0.38), inset 0 1px 0 rgba(255, 255, 255, 0.05);
  grid-column: 1;
  justify-self: start;
  align-self: start;
  transform: translateX(clamp(0.75rem, 10vw, 10.5rem));
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

@media (max-width: 1100px) {
  .hero {
    grid-template-columns: 1fr;
    justify-content: stretch;
    padding: calc(1.4rem + var(--hero-overlap)) clamp(1.4rem, 3vw, 2.4rem) 3.6rem;
  }

  .hero__content {
    grid-column: 1;
    justify-self: start;
    width: 100%;
  }
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
  .hero__content {
    transform: none;
  }
}
</style>
