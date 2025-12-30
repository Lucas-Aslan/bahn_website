<script setup lang="ts">
type CareerSignal = {
  title: string
  detail: string
  accent: 'gold' | 'cyan' | 'magenta'
}

type CareerStep = {
  badge: string
  title: string
  detail: string
}

const careerSignals: CareerSignal[] = [
  {
    title: 'Vollständige Unterlagen',
    detail: 'Lebenslauf, Qualifikationen und Nachweise sorgen für eine fundierte Entscheidung.',
    accent: 'gold'
  },
  {
    title: 'Fachliches Gespräch',
    detail: 'Persönlicher Austausch mit Disposition und Fachbereich zu Einsätzen und Erwartungen.',
    accent: 'cyan'
  },
  {
    title: 'Onboarding & Sicherheit',
    detail: 'Verbindliche Unterweisungen, dokumentierte Checks und klarer Starttermin.',
    accent: 'magenta'
  }
]

const careerSteps: CareerStep[] = [
  {
    badge: '1',
    title: 'Bewerbungsunterlagen senden',
    detail: 'Lebenslauf, Qualifikationen und Wunsch-Einsatzorte über unser Formular übermitteln.'
  },
  {
    badge: '2',
    title: 'Qualifikations- & Fachgespräch',
    detail: 'Persönliches Gespräch mit Fachverantwortlichen.'
  },
  {
    badge: '3',
    title: 'Onboarding & Einsatzstart',
    detail: 'Verbindliche Unterweisungen, ausgestattete Arbeitsmittel und klarer Einsatzplan.'
  }
]
</script>

<template>
  <section class="career section js-reveal">
    <div class="career__backdrop" aria-hidden="true">
      <span class="career__halo career__halo--gold" />
      <span class="career__halo career__halo--cyan" />
      <span class="career__gridlines" />
    </div>

    <div class="career__shell">
      <div class="career__eyebrow">
        <span class="career__spark" aria-hidden="true" />
        <p class="eyebrow">Karriere</p>
        <span class="career__eyebrow-pill">Strukturiertes Bewerbungsverfahren</span>
      </div>
      <div class="career__headline">
        <h2>Kompetent bewerben. Verlässlich starten.</h2>
        <p class="career__lead">
          Reiche vollständige Unterlagen ein, sprich mit uns über Deinen Werdegang und erhalte einen klaren Fahrplan
          für Deinen Einstieg.
        </p>
      </div>

      <div class="career__signals">
        <article
          v-for="signal in careerSignals"
          :key="signal.title"
          class="career-signal"
          :data-accent="signal.accent"
        >
          <span class="career-signal__glow" aria-hidden="true" />
          <span class="career-signal__pulse" aria-hidden="true" />
          <div class="career-signal__header">
            <span class="career-signal__badge">{{ signal.title }}</span>
            <span class="career-signal__icon" aria-hidden="true">✹</span>
          </div>
          <p class="career-signal__detail">{{ signal.detail }}</p>
        </article>
      </div>

      <div class="career-steps">
        <div
          v-for="step in careerSteps"
          :key="step.title"
          class="career-step"
        >
          <div class="career-step__badge">{{ step.badge }}</div>
          <div>
            <p class="career-step__title">{{ step.title }}</p>
            <p class="career-step__detail">{{ step.detail }}</p>
          </div>
        </div>
        <div class="career-steps__note">
          <span class="career-steps__pulse" aria-hidden="true" />
          Wir melden uns in 48h – dann geht&apos;s los.
        </div>
      </div>
      <div class="career__cta-row">
        <NuxtLink to="/kontakt" class="cta cta--solid career__cta">
          Jetzt bewerben
          <span aria-hidden="true">→</span>
        </NuxtLink>
      </div>
    </div>
  </section>
</template>
