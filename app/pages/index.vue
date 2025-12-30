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

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

:global(.section) {
  background: linear-gradient(145deg, rgba(255, 250, 243, 0.9), rgba(246, 241, 235, 0.95));
  border-radius: 24px;
  padding: clamp(1.5rem, 2vw, 2rem);
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.06);
}

:global(.section__header) {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.4rem;
  align-items: end;
}

:global(.section h2) {
  margin: 0.2rem 0 0.35rem;
  font-size: clamp(1.8rem, 3vw, 2.3rem);
  letter-spacing: -0.01em;
  color: var(--color-forest);
}

:global(.section__lead) {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.6;
}

:global(.eyebrow) {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--color-rose);
  font-size: 0.82rem;
  background: rgba(199, 117, 139, 0.12);
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
}

:global(.cta) {
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

:global(.cta--solid) {
  background: linear-gradient(120deg, var(--color-rose), var(--color-forest));
  color: #ffffff;
  box-shadow: 0 18px 45px rgba(199, 117, 139, 0.25), inset 0 1px 0 rgba(255, 255, 255, 0.4);
}

:global(.cta--solid:hover),
:global(.cta--solid:focus-visible) {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 60px rgba(0, 72, 49, 0.25);
}

:global(.cta--ghost) {
  background: rgba(0, 72, 49, 0.06);
  color: var(--color-forest);
  border-color: rgba(0, 72, 49, 0.2);
  backdrop-filter: blur(8px);
}

:global(.cta--ghost:hover),
:global(.cta--ghost:focus-visible) {
  transform: translateY(-1px);
  background: rgba(199, 117, 139, 0.12);
}

:global(.js-reveal) {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
  transition-delay: var(--reveal-delay, 0ms);
}

:global(.js-reveal.is-visible) {
  opacity: 1;
  transform: translateY(0);
}

@media (max-width: 700px) {
  :global(.cta) {
    width: 100%;
  }
}
</style>
