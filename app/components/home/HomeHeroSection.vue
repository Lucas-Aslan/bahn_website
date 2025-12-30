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
