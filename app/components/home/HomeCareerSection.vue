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

<style scoped>
.career {
  position: relative;
  overflow: hidden;
  background: radial-gradient(circle at 18% 12%, rgba(249, 210, 112, 0.14), transparent 32%),
    radial-gradient(circle at 78% 80%, rgba(0, 255, 255, 0.12), transparent 36%),
    linear-gradient(145deg, #060a14, #0c1528 50%, #060914);
  border: 1px solid rgba(255, 255, 255, 0.06);
  color: #f6f8fb;
  isolation: isolate;
  padding: clamp(1.2rem, 2vw, 1.8rem);
  border-radius: 22px;
  box-shadow: 0 24px 70px rgba(0, 0, 0, 0.5);
}

.career__backdrop {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.career__gridlines {
  position: absolute;
  inset: -20%;
  background:
    linear-gradient(90deg, rgba(255, 255, 255, 0.04) 1px, transparent 1px),
    linear-gradient(0deg, rgba(255, 255, 255, 0.04) 1px, transparent 1px);
  background-size: 220px 220px;
  opacity: 0.25;
  filter: blur(1px);
  transform: rotate(-2deg) scale(1.1);
}

.career__halo {
  position: absolute;
  width: 420px;
  height: 420px;
  filter: blur(80px);
  opacity: 0.65;
  mix-blend-mode: screen;
  animation: careerFloat 12s ease-in-out infinite alternate;
}

.career__halo--gold {
  top: -12%;
  left: -8%;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.28), transparent 50%);
}

.career__halo--cyan {
  bottom: -16%;
  right: -10%;
  background: radial-gradient(circle, rgba(0, 255, 255, 0.2), transparent 52%);
  animation-duration: 14s;
  animation-delay: 0.5s;
}

.career__shell {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 1rem;
}

.career__eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.35rem 0.8rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.08);
  width: fit-content;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.15);
}

.career__spark {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: radial-gradient(circle, #f9d270, #c99038);
  box-shadow:
    0 0 0 6px rgba(249, 210, 112, 0.2),
    0 0 0 14px rgba(249, 210, 112, 0.08);
  color: #f9d270;
  animation: pulse 1.4s ease-in-out infinite;
}

.career__eyebrow-pill {
  padding: 0.25rem 0.7rem;
  border-radius: 999px;
  background: rgba(0, 255, 255, 0.12);
  color: #74e3ff;
  font-weight: 800;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  font-size: 0.8rem;
  border: 1px solid rgba(0, 255, 255, 0.25);
}

.career__headline h2 {
  margin: 0.2rem 0 0.2rem;
  font-size: clamp(1.6rem, 3vw, 2.2rem);
  letter-spacing: -0.02em;
}

.career__lead {
  margin: 0;
  color: #dbe5ff;
  line-height: 1.6;
  font-size: 1.02rem;
  max-width: 720px;
}

.career__signals {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 0.9rem;
}

.career-signal {
  position: relative;
  overflow: hidden;
  padding: 1rem 0.9rem;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow:
    0 18px 40px rgba(0, 0, 0, 0.35),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  backdrop-filter: blur(8px);
  isolation: isolate;
  transition: transform 0.35s ease, box-shadow 0.35s ease, border-color 0.25s ease;
}

.career-signal__glow {
  position: absolute;
  inset: -30% -10% auto;
  height: 70%;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.16), transparent 55%);
  filter: blur(24px);
  opacity: 0.8;
  z-index: 0;
  transform: translate3d(0, 0, 0);
  animation: careerGlow 6s ease-in-out infinite;
}

.career-signal__pulse {
  position: absolute;
  inset: auto -20% -40% auto;
  width: 240px;
  height: 240px;
  background: radial-gradient(circle, rgba(0, 255, 255, 0.18), transparent 60%);
  filter: blur(18px);
  opacity: 0.7;
  z-index: 0;
  animation: careerGlow 5s ease-in-out infinite reverse;
}

.career-signal[data-accent='cyan'] .career-signal__glow {
  background: radial-gradient(circle, rgba(0, 255, 255, 0.16), transparent 55%);
}

.career-signal[data-accent='magenta'] .career-signal__glow {
  background: radial-gradient(circle, rgba(255, 135, 255, 0.18), transparent 55%);
}

.career-signal__header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.6rem;
  position: relative;
  z-index: 1;
}

.career-signal__badge {
  padding: 0.35rem 0.65rem;
  border-radius: 999px;
  background: rgba(0, 0, 0, 0.45);
  border: 1px solid rgba(255, 255, 255, 0.12);
  font-weight: 800;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: #f9d270;
  font-size: 0.85rem;
}

.career-signal__icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 34px;
  height: 34px;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.16);
  color: #fff;
  font-weight: 900;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.12);
}

.career-signal__detail {
  margin: 0.6rem 0 0;
  color: #dbe5ff;
  line-height: 1.6;
  position: relative;
  z-index: 1;
}

.career-signal:hover,
.career-signal:focus-within {
  transform: translateY(-6px) scale(1.01);
  border-color: rgba(249, 210, 112, 0.4);
  box-shadow:
    0 26px 60px rgba(0, 0, 0, 0.48),
    0 0 0 1px rgba(249, 210, 112, 0.16);
}

.career__cta-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
  align-items: center;
}

.career__cta {
  min-width: 220px;
  backdrop-filter: blur(10px);
}

.career-steps {
  display: grid;
  gap: 0.6rem;
  padding: 0.85rem 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08);
}

.career-step {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.75rem;
  align-items: center;
}

.career-step__badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 34px;
  height: 34px;
  border-radius: 12px;
  background: linear-gradient(140deg, rgba(249, 210, 112, 0.4), rgba(0, 255, 255, 0.28));
  color: #0a0f1c;
  font-weight: 900;
  border: 1px solid rgba(255, 255, 255, 0.18);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.18),
    0 14px 30px rgba(0, 0, 0, 0.28);
}

.career-step__title {
  margin: 0;
  font-weight: 800;
  letter-spacing: -0.01em;
}

.career-step__detail {
  margin: 0.12rem 0 0;
  color: #cfd9f2;
  line-height: 1.5;
}

.career-steps__note {
  position: relative;
  padding: 0.65rem 0.85rem;
  border-radius: 12px;
  background: rgba(249, 210, 112, 0.12);
  color: #f9e7be;
  font-weight: 800;
  overflow: hidden;
}

.career-steps__pulse {
  position: absolute;
  inset: -30% auto auto -10%;
  width: 180px;
  height: 180px;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.2), transparent 60%);
  filter: blur(14px);
  animation: careerGlow 5s ease-in-out infinite;
}

@keyframes careerGlow {
  0%,
  100% {
    transform: scale(1);
    opacity: 0.6;
  }
  50% {
    transform: scale(1.08);
    opacity: 1;
  }
}

@keyframes careerFloat {
  0% {
    transform: translateY(0) scale(1);
  }
  100% {
    transform: translateY(30px) scale(1.05);
  }
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

@media (max-width: 700px) {
  .career__cta {
    width: 100%;
    justify-content: center;
  }
}
</style>
