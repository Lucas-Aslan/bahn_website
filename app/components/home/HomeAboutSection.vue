<template>
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
</template>

<style scoped>
.about {
  position: relative;
  overflow: hidden;
  padding: clamp(2rem, 3vw, 2.8rem);
  background:
    linear-gradient(135deg, var(--color-paper), var(--color-cream)),
    radial-gradient(circle at 14% 20%, rgba(199, 117, 139, 0.16), transparent 40%),
    radial-gradient(circle at 82% 72%, rgba(0, 72, 49, 0.12), transparent 36%);
  border: 1px solid rgba(0, 72, 49, 0.14);
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.08);
  color: var(--color-ink);
  transform-style: preserve-3d;
  transform-origin: center center;
  transition:
    transform 0.9s cubic-bezier(0.2, 0.7, 0.15, 1),
    opacity 0.9s ease,
    filter 0.9s ease,
    box-shadow 0.9s ease;
}

.about h2 {
  color: var(--color-ink);
}

.about .section__lead {
  color: var(--color-muted);
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
  background: radial-gradient(circle at 30% 28%, rgba(199, 117, 139, 0.14), transparent 36%),
    radial-gradient(circle at 82% 62%, rgba(0, 72, 49, 0.14), transparent 32%);
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
  background: linear-gradient(105deg, rgba(199, 117, 139, 0.2), rgba(255, 255, 255, 0));
  filter: blur(24px);
  transform: translateY(32px) skewX(-12deg) scaleX(0.6);
  mix-blend-mode: multiply;
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
  filter: blur(8px) saturate(0.95);
}

.about.js-reveal.is-visible {
  transform: translateY(0) scale(1) rotateX(0deg);
  filter: blur(0) saturate(1.05);
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.12), 0 0 0 1px rgba(0, 72, 49, 0.08);
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
  color: var(--color-forest);
}

.about__spark {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--color-rose) 0%, rgba(199, 117, 139, 0.35) 70%, transparent 100%);
  box-shadow: 0 0 0 0 rgba(199, 117, 139, 0.45);
  animation: pulse 2.2s ease-in-out infinite;
}

.about__cta {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  font-weight: 700;
  color: var(--color-forest);
  text-decoration: none;
  margin-top: 0.2rem;
  padding: 0.65rem 1rem;
  border-radius: 12px;
  border: 1px solid rgba(0, 72, 49, 0.16);
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease, background 0.2s ease;
  backdrop-filter: blur(6px);
}

.about__cta:hover,
.about__cta:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
  border-color: rgba(0, 72, 49, 0.36);
  background: rgba(0, 72, 49, 0.08);
  text-decoration: none;
}

.about__cta--solid {
  background: var(--color-forest);
  color: #ffffff;
  border: 1px solid rgba(0, 72, 49, 0.28);
}

.about__cta--solid:hover,
.about__cta--solid:focus-visible {
  box-shadow: 0 12px 35px rgba(0, 72, 49, 0.2), 0 0 0 1px rgba(0, 72, 49, 0.18);
  transform: translateY(-2px) scale(1.01);
}

.about__cta--ghost {
  color: var(--color-forest);
  border-color: rgba(0, 72, 49, 0.18);
  background: rgba(0, 72, 49, 0.06);
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
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid rgba(0, 72, 49, 0.14);
  box-shadow: 0 12px 30px rgba(0, 0, 0, 0.08);
}

.about__pulse {
  margin-top: 0.12rem;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(0, 72, 49, 0.8), rgba(0, 72, 49, 0));
  box-shadow: 0 0 0 0 rgba(0, 72, 49, 0.32);
  animation: pulse 1.9s ease-in-out infinite;
}

.about__pulse--gold {
  background: radial-gradient(circle, rgba(199, 117, 139, 0.8), rgba(199, 117, 139, 0));
  box-shadow: 0 0 0 0 rgba(199, 117, 139, 0.32);
}

.about__pulse--cyan {
  background: radial-gradient(circle, rgba(0, 72, 49, 0.6), rgba(0, 72, 49, 0));
  box-shadow: 0 0 0 0 rgba(0, 72, 49, 0.32);
}

.about__label {
  margin: 0;
  font-weight: 700;
  letter-spacing: 0.01em;
  color: var(--color-ink);
}

.about__description {
  margin: 0.08rem 0 0;
  color: var(--color-muted);
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
</style>
