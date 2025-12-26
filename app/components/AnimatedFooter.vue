<template>
  <footer class="footer">
    <div class="footer__glow" aria-hidden="true" />
    <div class="footer__grid">
      <div class="footer__brand">
        <div class="footer__logo">
          <span class="footer__spark" aria-hidden="true" />
          <span class="footer__initials">BL</span>
        </div>
        <div>
          <p class="footer__eyebrow">Bahnlogistik</p>
          <p class="footer__title">RailPulse</p>
        </div>
        <p class="footer__tagline">
          Fortschrittliche Lösungen für Schienenverkehr, Infrastruktur und Logistik – präzise, sicher und mit
          goldener Effizienz.
        </p>

        <div class="footer__pills" role="list">
          <span class="footer__pill" role="listitem">24/7 Einsatzbereit</span>
          <span class="footer__pill" role="listitem">Zertifizierte Teams</span>
          <span class="footer__pill" role="listitem">Deutschlandweit</span>
        </div>
      </div>

      <div class="footer__columns">
        <div class="footer__column">
          <p class="footer__heading">Leistungen</p>
          <ul class="footer__list">
            <li><NuxtLink to="/leistungen/transport">Präzisions-Transport</NuxtLink></li>
            <li><NuxtLink to="/leistungen/infrastruktur">Infrastruktur-Bau</NuxtLink></li>
            <li><NuxtLink to="/leistungen/logistik">Terminal &amp; Logistik</NuxtLink></li>
          </ul>
        </div>

        <div class="footer__column">
          <p class="footer__heading">Unternehmen</p>
          <ul class="footer__list">
            <li><NuxtLink to="/about">Über uns</NuxtLink></li>
            <li><NuxtLink to="/kontakt">Kontakt</NuxtLink></li>
            <li><NuxtLink to="/karriere">Karriere</NuxtLink></li>
          </ul>
        </div>

        <div class="footer__column">
          <p class="footer__heading">Direktkontakt</p>
          <div class="footer__card">
            <p class="footer__card-label">Projektbriefing</p>
            <p class="footer__card-text">Schnelle Abstimmung mit einem Lead-Ingenieur.</p>
            <NuxtLink to="/kontakt" class="footer__cta">Termin sichern</NuxtLink>
          </div>
        </div>
      </div>
    </div>

    <div class="footer__meta">
      <div class="footer__ticker" aria-hidden="true">
        <span class="footer__pulse" />
        <span>Next departure in: 02:45</span>
        <span>Netzstabilität: 99.98%</span>
        <span>Flotten-Tracking aktiv</span>
      </div>
      <p class="footer__legal">© 2024 RailPulse Bahnlogistik – Präzision auf Schienen.</p>
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
  background:
    radial-gradient(circle at 30% 60%, rgba(249, 210, 112, 0.12), transparent 30%),
    radial-gradient(circle at 80% 10%, rgba(255, 255, 255, 0.05), transparent 34%);
  filter: blur(35px);
  opacity: 0.8;
  animation: glowShift 9s ease-in-out infinite alternate;
  pointer-events: none;
  z-index: 0;
}

.footer__grid {
  position: relative;
  z-index: 1;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.8rem;
  align-items: start;
}

.footer__brand {
  display: grid;
  gap: 0.8rem;
}

.footer__logo {
  position: relative;
  width: 64px;
  height: 64px;
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

.footer__columns {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 1.2rem;
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
  padding-left: 0.9rem;
  transition: color 0.2s ease, transform 0.2s ease;
}

.footer__list a::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.6em;
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

.footer__meta {
  position: relative;
  z-index: 1;
  margin-top: 1.8rem;
  border-top: 1px solid rgba(255, 255, 255, 0.06);
  padding-top: 1rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
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
}

.footer__pulse {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f9d270;
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.6);
  animation: pulse 2.8s infinite;
}

.footer__legal {
  margin: 0;
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

@media (max-width: 720px) {
  .footer {
    margin: 1rem 1rem 2rem;
  }

  .footer__grid {
    grid-template-columns: 1fr;
  }

  .footer__ticker {
    width: 100%;
    justify-content: center;
  }

  .footer__meta {
    flex-direction: column;
  }
}
</style>
