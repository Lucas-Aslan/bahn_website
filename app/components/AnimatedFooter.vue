<template>
  <footer class="footer">
    <div class="footer__glow" aria-hidden="true" />

    <div class="footer__grid">
      <div class="footer__brand">
        <div class="footer__brand-head">

          <div class="footer__brand-text">
            <p class="footer__eyebrow">Bahnlogistik</p>
            <p class="footer__title">Babylon Bahndienste</p>
          </div>
        </div>


        <div class="footer__card footer__contact-card">
          <span class="footer__badge">24/7 Leitstelle</span>
          <p class="footer__card-label">Kontakt</p>
          <p class="footer__card-text">
            Babylon Bahndienste UG (haftungsbeschränkt)<br>
            Frankfurter Weg 27<br>
            33106 Paderborn
          </p>
          <div class="footer__contact-links">
            <span>Telefon: <a href="tel:+49123456789">+49 123 456 789</a></span>
            <span>E-Mail: <a href="mailto:info@babylon-bahndienste.de">info@babylon-bahndienste.de</a></span>
          </div>
          <div class="footer__contact-actions" aria-label="Direkte Kontaktoptionen">
            <a class="footer__action" href="tel:+49123456789">
              <span class="footer__action-dot" aria-hidden="true" />
              Jetzt anrufen
            </a>
            <a class="footer__action" href="mailto:info@babylon-bahndienste.de">
              <span class="footer__action-dot" aria-hidden="true" />
              E-Mail senden
            </a>
          </div>
          <NuxtLink to="/kontakt" class="footer__cta">Kontakt aufnehmen</NuxtLink>
        </div>
      </div>

      <div class="footer__columns">
        <div class="footer__column">
          <p class="footer__heading">Unternehmen</p>
          <ul class="footer__list">
            <li><NuxtLink to="/about">Über uns</NuxtLink></li>
            <li><NuxtLink to="/karriere">Karriere</NuxtLink></li>
            <li><NuxtLink to="/kontakt">Kontakt</NuxtLink></li>
          </ul>
        </div>

        <div class="footer__column">
          <p class="footer__heading">Rechtliches</p>
          <ul class="footer__list">
            <li><NuxtLink to="/impressum">Impressum</NuxtLink></li>
            <li><NuxtLink to="/datenschutz">Datenschutz</NuxtLink></li>
            <li><NuxtLink to="/barrierefreiheit">Barrierefreiheit</NuxtLink></li>
          </ul>
        </div>
      </div>
    </div>

    <div class="footer__meta">
      <div class="footer__ticker">
        <span class="footer__pulse" aria-hidden="true" />
        <p class="footer__legal">© 2026 Babylon Bahndienste – Präzision auf Schienen.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  position: relative;
  margin: 2rem 1.5rem 3rem;
  padding: 2.4rem clamp(1rem, 4vw, 2.6rem);
  border-radius: 24px;
  background: radial-gradient(circle at 16% 18%, rgba(249, 210, 112, 0.12), transparent 38%),
    radial-gradient(circle at 86% 32%, rgba(201, 144, 56, 0.1), transparent 40%),
    rgba(7, 9, 16, 0.92);
  box-shadow: 0 35px 90px rgba(0, 0, 0, 0.65), inset 0 1px 0 rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.16);
  overflow: hidden;
  isolation: isolate;
}

.footer__glow {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 60%, rgba(249, 210, 112, 0.12), transparent 30%),
    radial-gradient(circle at 80% 10%, rgba(255, 255, 255, 0.05), transparent 34%);
  filter: blur(35px);
  opacity: 0.8;
  animation: glowShift 9s ease-in-out infinite alternate;
  pointer-events: none;
  z-index: 0;
}

/* ---------- Layout (responsive) ---------- */
.footer__grid {
  position: relative;
  z-index: 1;
  display: grid;
  gap: 1.8rem;
  align-items: start;
  /* Mobile-first: eine Spalte */
  grid-template-columns: 1fr;
}

.footer__brand,
.footer__columns {
  min-width: 0; /* verhindert Overflow in Grid */
}

@media (min-width: 960px) {
  .footer__grid {
    grid-template-columns: minmax(0, 1.1fr) minmax(0, 1fr);
    gap: 2.2rem;
  }
}

.footer__brand {
  display: grid;
  gap: 0.9rem;
}

.footer__brand-head {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.footer__brand-text {
  min-width: 0;
}

.footer__logo {
  position: relative;
  width: 64px;
  height: 64px;
  flex: 0 0 auto;
  border-radius: 18px;
  background: linear-gradient(135deg, #f9d270, #c99038);
  box-shadow: 0 20px 45px rgba(249, 210, 112, 0.36);
  display: grid;
  place-items: center;
  overflow: hidden;
}

.footer__initials {
  font-weight: 800;
  color: #0c0a05;
  letter-spacing: 0.08em;
  z-index: 1;
}

.footer__spark {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 30% 30%, rgba(255, 255, 255, 0.8), transparent 35%);
  filter: blur(8px);
  mix-blend-mode: screen;
  animation: sparkRotate 12s linear infinite;
}

.footer__eyebrow {
  margin: 0;
  color: #f6e6b4;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  font-size: 0.78rem;
}

.footer__title {
  margin: 0;
  font-size: 1.4rem;
  font-weight: 800;
  letter-spacing: 0.01em;
}

.footer__tagline {
  margin: 0.1rem 0 0.8rem;
  color: #dce7ff;
  line-height: 1.6;
}

.footer__pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.footer__pill {
  padding: 0.45rem 0.8rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.25);
  color: #f9d270;
  font-weight: 600;
  font-size: 0.9rem;
  position: relative;
  overflow: hidden;
}

.footer__pill::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transform: translateX(-100%);
  animation: shimmer 3.6s ease-in-out infinite;
}

/* Columns: Mobile-first 1 Spalte, dann 2, dann 3 */
.footer__columns {
  display: grid;
  gap: 1.2rem;
  grid-template-columns: 1fr;
}

@media (min-width: 640px) {
  .footer__columns {
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}

@media (min-width: 960px) {
  .footer__columns {
    grid-template-columns: repeat(2, minmax(0, 1fr));
    justify-self: end;
    align-self: center;
    margin-top: 0.9rem;
    padding-right: 0.8rem;
    width: fit-content;
  }
}

@media (min-width: 1200px) {
  .footer__columns {
    gap: 1.5rem;
    grid-template-columns: repeat(2, minmax(0, 1.05fr));
  }
}

.footer__heading {
  margin: 0 0 0.6rem;
  color: #f6e6b4;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-size: 0.86rem;
}

.footer__list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.45rem;
}

.footer__list a {
  color: #e8f0ff;
  text-decoration: none;
  font-weight: 600;
  position: relative;
  padding: 0.15rem 0 0.15rem 0.9rem;
  transition: color 0.2s ease, transform 0.2s ease;
  line-height: 1.35;
  display: inline-block;
  max-width: 100%;
}

.footer__list a::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.62em;
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: linear-gradient(120deg, #f9d270, #c99038);
  box-shadow: 0 0 12px rgba(249, 210, 112, 0.6);
  transform: scale(0.8);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.footer__list a:hover,
.footer__list a:focus-visible {
  color: #ffffff;
  transform: translateX(4px);
}

.footer__list a:hover::before,
.footer__list a:focus-visible::before {
  transform: scale(1);
  box-shadow: 0 0 18px rgba(249, 210, 112, 0.8);
}

.footer__card {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(249, 210, 112, 0.2);
  border-radius: 14px;
  padding: 1rem 1.1rem;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.05), 0 14px 40px rgba(0, 0, 0, 0.35);
  display: grid;
  gap: 0.35rem;
  position: relative;
  overflow: hidden;
}

.footer__card::after {
  content: '';
  position: absolute;
  inset: -30% -10% auto;
  height: 60%;
  background: linear-gradient(120deg, rgba(249, 210, 112, 0.18), transparent);
  filter: blur(25px);
  opacity: 0.8;
  animation: cardGlow 6s ease-in-out infinite alternate;
  pointer-events: none;
}

.footer__card-label {
  margin: 0;
  color: #f9d270;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.footer__card-text {
  margin: 0;
  color: #dce7ff;
}

.footer__contact-card {
  gap: 0.7rem;
}

.footer__contact-links {
  display: grid;
  gap: 0.35rem;
}

.footer__badge {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  width: fit-content;
  padding: 0.35rem 0.65rem;
  border-radius: 999px;
  background: rgba(249, 210, 112, 0.12);
  border: 1px solid rgba(249, 210, 112, 0.35);
  color: #f9d270;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
  font-size: 0.78rem;
}

.footer__contact-actions {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 0.45rem;
}

.footer__action {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.55rem 0.75rem;
  border-radius: 10px;
  border: 1px solid rgba(249, 210, 112, 0.18);
  background: rgba(255, 255, 255, 0.03);
  color: #ffffff;
  font-weight: 700;
  text-decoration: none;
  transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease;
}

.footer__action:hover,
.footer__action:focus-visible {
  transform: translateY(-1px);
  border-color: rgba(249, 210, 112, 0.32);
  background: rgba(249, 210, 112, 0.08);
}

.footer__action-dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: linear-gradient(120deg, #f9d270, #c99038);
  box-shadow: 0 0 12px rgba(249, 210, 112, 0.65);
}

.footer__card a {
  color: #ffffff;
  font-weight: 700;
  text-decoration: none;
}

.footer__card a:hover,
.footer__card a:focus-visible {
  text-decoration: underline;
  text-decoration-thickness: 2px;
  text-underline-offset: 3px;
}

.footer__cta {
  width: fit-content;
  padding: 0.65rem 0.95rem;
  border-radius: 12px;
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  font-weight: 800;
  text-decoration: none;
  box-shadow: 0 12px 30px rgba(249, 210, 112, 0.35);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.footer__cta:hover,
.footer__cta:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 16px 40px rgba(201, 144, 56, 0.4);
}

/* Meta: immer sauber umbrechen, auf Mobile zentrieren */
.footer__meta {
  position: relative;
  z-index: 1;
  margin-top: 1.8rem;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
  padding-top: 1rem;
  display: flex;
  flex-wrap: wrap;
  gap: 0.8rem;
  color: #cfe2ff;
  font-size: 0.95rem;
}

.footer__ticker {
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  padding: 0.6rem 0.8rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(249, 210, 112, 0.18);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
  max-width: 100%;
}

.footer__pulse {
  width: 10px;
  height: 10px;
  flex: 0 0 auto;
  border-radius: 50%;
  background: #f9d270;
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.6);
  animation: pulse 2.8s infinite;
}

.footer__legal {
  margin: 0;
  min-width: 0;
  overflow-wrap: anywhere;
}

@media (max-width: 720px) {
  .footer {
    margin: 1rem 1rem 2rem;
    padding: 1.8rem 1.1rem;
  }

  .footer__brand-head {
    gap: 0.85rem;
  }

  .footer__title {
    font-size: 1.25rem;
  }

  .footer__ticker {
    width: 100%;
    justify-content: center;
    text-align: center;
  }

  .footer__meta {
    justify-content: center;
  }
}

/* Extra-small: CTA & Pills noch kompakter */
@media (max-width: 420px) {
  .footer__pill {
    font-size: 0.86rem;
    padding: 0.4rem 0.7rem;
  }

  .footer__cta {
    width: 100%;
    text-align: center;
  }
}

@keyframes glowShift {
  from {
    transform: translate3d(-8px, 6px, 0);
  }
  to {
    transform: translate3d(12px, -10px, 0);
  }
}

@keyframes sparkRotate {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(180deg) scale(1.05);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes shimmer {
  0% {
    transform: translateX(-100%);
  }
  50% {
    transform: translateX(120%);
  }
  100% {
    transform: translateX(120%);
  }
}

@keyframes pulse {
  0% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.5);
  }
  70% {
    transform: scale(1.08);
    box-shadow: 0 0 0 14px rgba(249, 210, 112, 0);
  }
  100% {
    transform: scale(0.95);
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0);
  }
}

@keyframes cardGlow {
  from {
    transform: translate3d(-12px, 4px, 0) rotate(-2deg);
  }
  to {
    transform: translate3d(18px, -6px, 0) rotate(3deg);
  }
}
</style>
