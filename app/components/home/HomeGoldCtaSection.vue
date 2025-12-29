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
    radial-gradient(circle at 18% 20%, rgba(249, 210, 112, 0.22), transparent 34%),
    radial-gradient(circle at 78% 68%, rgba(249, 210, 112, 0.18), transparent 34%),
    linear-gradient(135deg, #0e0a06, #1a1208 55%, #0f0a05);
  color: #f9edd0;
  border: 1px solid rgba(249, 210, 112, 0.26);
  box-shadow: 0 30px 90px rgba(0, 0, 0, 0.55), inset 0 1px 0 rgba(255, 255, 255, 0.12);
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
  background: radial-gradient(circle at 28% 20%, rgba(249, 210, 112, 0.16), transparent 50%),
    linear-gradient(180deg, rgba(255, 255, 255, 0.05), rgba(0, 0, 0, 0.5));
  border-radius: 18px;
  border: 1px solid rgba(249, 210, 112, 0.22);
  padding: clamp(0.9rem, 2vw, 1.2rem);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.06),
    0 18px 40px rgba(0, 0, 0, 0.35);
}

.gold-cta__image {
  width: 100%;
  height: auto;
  display: block;
  border-radius: 14px;
  box-shadow:
    0 14px 30px rgba(0, 0, 0, 0.4),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
}

.gold-cta__legend {
  display: flex;
  align-items: center;
  gap: 0.55rem;
  color: #f4e3b8;
  font-size: 0.95rem;
  margin-top: 0.2rem;
}

.gold-cta__legend-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f9d270;
  box-shadow: 0 0 14px rgba(249, 210, 112, 0.6);
}

.gold-cta__content {
  background: rgba(8, 6, 4, 0.7);
  border-radius: 16px;
  padding: clamp(1.2rem, 2.5vw, 1.8rem);
  border: 1px solid rgba(249, 210, 112, 0.28);
  box-shadow:
    0 18px 50px rgba(0, 0, 0, 0.45),
    inset 0 1px 0 rgba(255, 255, 255, 0.08);
  display: grid;
  gap: 0.85rem;
}

.gold-cta__eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.06em;
  font-weight: 800;
  font-size: 0.9rem;
  color: #f9d270;
}

.gold-cta h2 {
  margin: 0;
  font-size: clamp(1.95rem, 3vw, 2.4rem);
  letter-spacing: -0.01em;
  color: #fff6dd;
}

.gold-cta__lead {
  margin: 0;
  color: #f4e3b8;
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
  background: rgba(255, 255, 255, 0.08);
  color: #f9edd0;
  border: 1px solid rgba(249, 210, 112, 0.22);
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
  border: 1px solid rgba(249, 210, 112, 0.4);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.35);
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease, color 0.2s ease;
}

.gold-cta__button--solid {
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
}

.gold-cta__button--ghost {
  background: rgba(255, 255, 255, 0.06);
  color: #f9edd0;
}

.gold-cta__button:hover,
.gold-cta__button:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 55px rgba(0, 0, 0, 0.45);
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
