<template>
  <section class="gold-cta section js-reveal">
    <div class="gold-cta__grid">
      <figure class="gold-cta__media">
        <img
          src="/images/cta-bild.jpg"
          alt="Ops Desk Übersicht von Babylon Bahndiensten"
          class="gold-cta__image"
          loading="lazy"
        >
        <figcaption class="gold-cta__legend">
          <span class="gold-cta__legend-dot" aria-hidden="true" />
          Live gesteuerte Einsätze &amp; Crew-Übersicht
        </figcaption>
      </figure>

      <div class="gold-cta__content">
        <p class="gold-cta__eyebrow">Mit Babylon Bahndienste durchstarten</p>
        <h2>Präzise Bahnlogistik – klar gesteuert, schnell gestartet.</h2>
        <p class="gold-cta__lead">
          Zuverlässige Crews, klare Abläufe und direkte Ansprechpartner. Wir übernehmen Personalgestellung,
          Consulting und operative Steuerung – präzise, sicher und deutschlandweit.
        </p>
        <div class="gold-cta__actions">
          <NuxtLink to="/kontakt" class="gold-cta__button gold-cta__button--solid">
            Kontaktieren
            <span aria-hidden="true">↗</span>
          </NuxtLink>
          <NuxtLink to="/karriere" class="gold-cta__button gold-cta__button--ghost">
            Starte deine Karriere
            <span aria-hidden="true">↗</span>
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.gold-cta {
  position: relative;
  overflow: hidden;
  background:
    radial-gradient(circle at 18% 20%, rgba(199, 117, 139, 0.16), transparent 42%),
    radial-gradient(circle at 82% 72%, rgba(0, 72, 49, 0.12), transparent 42%),
    linear-gradient(135deg, var(--color-paper), var(--color-cream));
  color: var(--color-ink);
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow:
    0 30px 80px rgba(0, 0, 0, 0.08),
    inset 0 0 0 1px rgba(255, 255, 255, 0.5);
  border-radius: 24px;
  isolation: isolate;
  padding: clamp(2rem, 3vw, 2.8rem);
}

.gold-cta__grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  gap: clamp(1.4rem, 2vw, 2rem);
  align-items: center;
}

.gold-cta__media {
  margin: 0;
  background:
    radial-gradient(circle at 28% 20%, rgba(199, 117, 139, 0.12), transparent 52%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.75), rgba(255, 250, 243, 0.65));
  border-radius: 18px;
  border: 1px solid rgba(0, 72, 49, 0.12);
  padding: clamp(0.9rem, 2vw, 1.2rem);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.8),
    0 18px 45px rgba(0, 0, 0, 0.08);
}

.gold-cta__image {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 14px;
  box-shadow:
    0 14px 30px rgba(0, 0, 0, 0.1),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
}

.gold-cta__legend {
  display: flex;
  align-items: center;
  gap: 0.55rem;
  color: var(--color-muted);
  font-size: 0.95rem;
  margin-top: 0.2rem;
}

.gold-cta__legend-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: var(--color-rose);
  box-shadow: 0 0 14px rgba(199, 117, 139, 0.35);
}

.gold-cta__content {
  background: rgba(255, 250, 243, 0.86);
  border-radius: 16px;
  padding: clamp(1.2rem, 2.5vw, 1.8rem);
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow:
    0 18px 50px rgba(0, 0, 0, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
  display: grid;
  gap: 0.85rem;
}

.gold-cta__eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  font-weight: 800;
  font-size: 0.9rem;
  color: var(--color-forest);
}

.gold-cta h2 {
  margin: 0;
  font-size: clamp(1.95rem, 3vw, 2.4rem);
  letter-spacing: -0.01em;
  color: var(--color-ink);
}

.gold-cta__lead {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.6;
  font-size: 1.05rem;
}

.gold-cta__highlights {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.gold-cta__chip {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.45rem 0.9rem;
  border-radius: 999px;
  background: rgba(0, 72, 49, 0.06);
  color: var(--color-forest);
  border: 1px solid rgba(0, 72, 49, 0.18);
  font-weight: 700;
  letter-spacing: 0.02em;
}

.gold-cta__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.85rem;
  align-items: center;
}

.gold-cta__button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.35rem;
  padding: 0.95rem 1.25rem;
  border-radius: 14px;
  font-weight: 800;
  text-decoration: none;
  letter-spacing: 0.01em;
  border: 1px solid rgba(0, 72, 49, 0.18);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.08);
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease, color 0.2s ease;
}

.gold-cta__button--solid {
  background: var(--color-forest);
  color: #ffffff;
  box-shadow: 0 18px 45px rgba(0, 72, 49, 0.25);
}

.gold-cta__button--ghost {
  background: rgba(0, 72, 49, 0.08);
  color: var(--color-forest);
  border-color: rgba(0, 72, 49, 0.3);
}

.gold-cta__button:hover,
.gold-cta__button:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 55px rgba(0, 0, 0, 0.12);
}

@media (max-width: 700px) {
  .gold-cta__grid {
    grid-template-columns: 1fr;
  }

  .gold-cta__actions {
    flex-direction: column;
    align-items: stretch;
  }

  .gold-cta__button {
    width: 100%;
    justify-content: center;
    text-align: center;
  }
}
</style>
