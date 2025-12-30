<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

import HomeAboutSection from '~/components/home/HomeAboutSection.vue'
import HomeCareerSection from '~/components/home/HomeCareerSection.vue'
import HomeFaqSection from '~/components/home/HomeFaqSection.vue'
import HomeGoldCtaSection from '~/components/home/HomeGoldCtaSection.vue'
import HomeHeroSection from '~/components/home/HomeHeroSection.vue'
import HomePerformanceSection from '~/components/home/HomePerformanceSection.vue'
import HomeServiceSection from '~/components/home/HomeServiceSection.vue'

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
    element.style.setProperty('--reveal-delay', `${index * 80}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="page">
    <HomeHeroSection />
    <HomeAboutSection />
    <HomePerformanceSection />
    <HomeCareerSection />
    <HomeGoldCtaSection />
    <HomeFaqSection />
    <HomeServiceSection />
  </div>
</template>
