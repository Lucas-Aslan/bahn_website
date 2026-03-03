<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

type Benefit = {
  title: string
  description: string
}

type Position = {
  title: string
  type: string
  schedule: string
  description: string
}

const benefits: Benefit[] = [
{
    title: 'Hansefit inklusive',
    description: 'Mit Hansefit trainierst du flexibel bei vielen Partnern und stärkst aktiv deine Gesundheit.'
  },
  {
    title: 'Modernes Auto für alle',
    description: 'Jede:r Mitarbeitende erhält ein sehr modernes Dienstfahrzeug für einen komfortablen Arbeitsalltag.'
  },
  {
    title: 'Planbare Einsätze',
    description: 'Strukturierte Schichtplanung mit verlässlicher Abstimmung durch feste Ansprechpartner:innen.'
  },
  {
    title: 'Moderne Arbeitsmittel',
    description: 'Digitale Einsatzsteuerung, hochwertige PSA und klar dokumentierte Sicherheitsprozesse.'
  },
  {
    title: 'Entwicklung mit Perspektive',
    description: 'Weiterbildungen und Qualifizierungen – vom Quereinstieg bis zur Führungsverantwortung.'
  },
  {
    title: 'Starkes Team',
    description: 'Respektvolle Zusammenarbeit, kurze Entscheidungswege und gelebte Verantwortung im Betrieb.'
  }

]

const positions: Position[] = [
  {
    title: 'Triebfahrzeugführer:in (m/w/d) – Cargo & Bau',
    type: 'Vollzeit',
    schedule: 'Schichtdienst',
    description: 'Du führst moderne Triebfahrzeuge im Güter- und Bauzugverkehr und sorgst für sichere Abläufe.'
  },
  {
    title: 'Rangierbegleiter:in (m/w/d)',
    type: 'Vollzeit',
    schedule: 'Tag / Nacht',
    description: 'Du unterstützt Rangierfahrten auf Werks- und Baustellengleisen mit Fokus auf Sicherheit und Qualität.'
  },
  {
    title: 'Wagenprüfer:in (m/w/d)',
    type: 'Vollzeit',
    schedule: 'Flexibel',
    description: 'Du führst Wagenprüfungen durch, dokumentierst nachvollziehbar und stellst die Betriebssicherheit sicher.'
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
  <div class="career-page">
    <section class="career-hero section js-reveal">
      <div class="career-hero__content">
        <p class="eyebrow">Karriere bei Babylon Bahndienste</p>
        <h1>Dein nächster Karriereschritt im Bahnbetrieb.</h1>
        <p class="section__lead">
          Wir verbinden Sicherheit, Verlässlichkeit und moderne Arbeitsbedingungen. Ob Einstieg, Quereinstieg oder
          nächster Entwicklungsschritt: Bei uns findest du ein professionelles Umfeld mit klarer Perspektive.
        </p>
        <div class="career-hero__actions">
          <a href="#jobs" class="cta cta--solid">Stellenangebote ansehen</a>
          <NuxtLink to="/kontakt" class="cta cta--ghost">Initiativ bewerben</NuxtLink>
        </div>
      </div>
      <div class="career-hero__image-wrap">
        <img src="/images/cta-bild.jpg" alt="Team von Babylon Bahndienste" class="career-hero__image" loading="lazy">
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Deine Vorteile</p>
          <h2>Warum Babylon Bahndienste?</h2>
          <p class="section__lead">Professionelle Rahmenbedingungen, menschliche Kultur und langfristige Perspektiven.</p>
        </div>
      </div>
      <div class="benefit-grid">
        <article v-for="benefit in benefits" :key="benefit.title" class="benefit-card">
          <h3>{{ benefit.title }}</h3>
          <p>{{ benefit.description }}</p>
        </article>
      </div>
    </section>

    <section id="jobs" class="section js-reveal">
      <div class="section__header section__header--split">
        <div>
          <p class="eyebrow">Offene Positionen</p>
          <h2>Werde Teil unseres Teams</h2>
          <p class="section__lead">
            Wir suchen engagierte Kolleg:innen mit Verantwortungsbewusstsein und Freude an sicherheitskritischer Arbeit.
          </p>
        </div>
        <NuxtLink to="/kontakt" class="cta cta--solid">Jetzt Kontakt aufnehmen</NuxtLink>
      </div>

      <div class="jobs-grid">
        <article v-for="position in positions" :key="position.title" class="job-card">
          <p class="job-card__meta">{{ position.type }} · {{ position.schedule }}</p>
          <h3>{{ position.title }}</h3>
          <p>{{ position.description }}</p>
          <NuxtLink to="/kontakt" class="text-link">Gespräch anfragen →</NuxtLink>
        </article>
      </div>
    </section>

    <section class="section section--cta js-reveal">
      <div>
        <p class="eyebrow">Initiativbewerbung</p>
        <h2>Nichts Passendes gefunden?</h2>
        <p class="section__lead">
          Sende uns trotzdem deine Bewerbung. Wir prüfen gemeinsam, wie dein Profil zu unseren Einsätzen passt.
        </p>
      </div>
      <NuxtLink to="/kontakt" class="cta cta--solid">Initiativ bewerben</NuxtLink>
    </section>
  </div>
</template>

<style scoped>
.career-page {
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
  background: rgba(199, 117, 139, 0.12);
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
  box-shadow: 0 18px 45px rgba(199, 117, 139, 0.28);
}

.cta--ghost {
  background: #ffffff;
  color: var(--color-forest);
  border-color: var(--color-border);
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
.career-hero {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(199, 117, 139, 0.12), rgba(0, 72, 49, 0.08));
  border-radius: 24px;
}

.career-hero__content h1 {
  margin: 0.2rem 0 0.45rem;
  font-size: clamp(2rem, 3vw, 2.6rem);
  color: var(--color-forest);
}

.career-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1rem;
}

.career-hero__image-wrap {
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid var(--color-border);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.1);
}

.career-hero__image {
  width: 100%;
  height: 100%;
  min-height: 260px;
  object-fit: cover;
  display: block;
}

.benefit-grid,
.jobs-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 1rem;
}

.benefit-card,
.job-card {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: 18px;
  padding: 1rem;
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.06);
}

.benefit-card h3,
.job-card h3 {
  margin: 0;
  color: var(--color-forest);
}

.benefit-card p,
.job-card p {
  margin: 0.45rem 0 0;
  color: var(--color-muted);
  line-height: 1.55;
}

.job-card__meta {
  margin: 0;
  font-size: 0.85rem;
  color: var(--color-rose);
  font-weight: 700;
}

.text-link {
  margin-top: 0.9rem;
  display: inline-flex;
  text-decoration: none;
  font-weight: 700;
  color: var(--color-forest);
}

.section--cta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  background: linear-gradient(135deg, rgba(0, 72, 49, 0.08), rgba(199, 117, 139, 0.12));
  border-radius: 24px;
}

@media (max-width: 900px) {
  .career-hero {
    grid-template-columns: 1fr;
  }

  .section--cta {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>
