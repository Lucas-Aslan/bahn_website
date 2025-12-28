<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'

type Spotlight = {
  x: number
  y: number
}

const services = [
  'Leistungsdisposition & Einsatzsteuerung',
  'Triebfahrzeugführer & Rangierpersonal',
  'Gleisbau & Infrastruktur-Begleitung',
  'Terminal- & Hafenlogistik',
  'Sicherheitskonzepte & Audits',
  'Beratung & Projektstart'
]

const spotlight = ref<Spotlight>({ x: 50, y: 50 })
const submitted = ref(false)
const shimmerInterval = ref<number | null>(null)

const handlePointerMove = (event: PointerEvent) => {
  const target = event.currentTarget as HTMLElement | null
  if (!target) return

  const rect = target.getBoundingClientRect()
  const x = ((event.clientX - rect.left) / rect.width) * 100
  const y = ((event.clientY - rect.top) / rect.height) * 100
  spotlight.value = { x, y }
}

const handleSubmit = (event: Event) => {
  event.preventDefault()
  submitted.value = true
  window.setTimeout(() => {
    submitted.value = false
  }, 4200)
}

onMounted(() => {
  shimmerInterval.value = window.setInterval(() => {
    spotlight.value = {
      x: Math.random() * 100,
      y: Math.random() * 100
    }
  }, 2600)
})

onBeforeUnmount(() => {
  if (shimmerInterval.value) {
    window.clearInterval(shimmerInterval.value)
  }
})
</script>

<template>
  <div class="kontakt-page" @pointermove="handlePointerMove">
    <div class="kontakt-grid" aria-hidden="true">
      <span class="grid-line" />
      <span class="grid-line grid-line--horizontal" />
    </div>

    <section class="kontakt-hero">
      <div class="hero-header">
        <p class="eyebrow">Kontakt</p>
        <h1>Gemeinsam fahren wir Ihre Projekte sicher ins Ziel.</h1>
        <p class="lede">
          Präzise Bahndienstleistungen, klare Absprachen und schnelle Reaktionszeiten. Teilen Sie uns Ihr Vorhaben mit –
          wir setzen uns zeitnah mit Ihnen in Verbindung.
        </p>

        <div class="signal-row" role="list">
          <span class="signal-chip" role="listitem">
            <span class="pulse" aria-hidden="true" /> 24/7 Bereitschaft
          </span>
          <span class="signal-chip" role="listitem">
            <span class="pulse pulse--cyan" aria-hidden="true" /> Sicherheitszertifizierte Teams
          </span>
          <span class="signal-chip" role="listitem">
            <span class="pulse pulse--magenta" aria-hidden="true" /> Bundesweit einsatzbereit
          </span>
        </div>
      </div>

      <div class="kontakt-panels">
        <form class="kontakt-form" @submit="handleSubmit">
          <div class="form-grid">
            <label class="field">
              <span>Vorname</span>
              <input name="firstName" type="text" placeholder="Ihr Name" autocomplete="given-name">
            </label>
            <label class="field">
              <span>Nachname *</span>
              <input name="lastName" type="text" placeholder="Nachname" autocomplete="family-name" required>
            </label>
            <label class="field">
              <span>Firma</span>
              <input name="company" type="text" placeholder="Unternehmen" autocomplete="organization">
            </label>
            <label class="field">
              <span>E-Mail *</span>
              <input name="email" type="email" placeholder="name@unternehmen.de" autocomplete="email" required>
            </label>
            <label class="field">
              <span>Telefonnummer *</span>
              <input name="phone" type="tel" placeholder="+49" autocomplete="tel" required>
            </label>
            <label class="field">
              <span>Leistung *</span>
              <select name="service" required>
                <option value="">Leistung auswählen</option>
                <option v-for="service in services" :key="service" :value="service">
                  {{ service }}
                </option>
              </select>
            </label>
          </div>

          <label class="field field--wide">
            <span>Nachricht</span>
            <textarea
              name="message"
              rows="4"
              placeholder="Beschreiben Sie Ihr Vorhaben, Zeitplan und Einsatzort."
            ></textarea>
          </label>

          <div class="form-actions">
            <label class="toggle">
              <input type="checkbox" name="callback" checked>
              <span class="toggle-slider" aria-hidden="true" />
              <span class="toggle-label">Bitte um Rückruf</span>
            </label>
            <button type="submit" class="cta">
              <span>{{ submitted ? 'Nachricht gesendet' : 'Abschicken' }}</span>
              <span class="cta-icon" aria-hidden="true">↗</span>
            </button>
          </div>

          <p v-if="submitted" class="hint success">
            Vielen Dank! Wir melden uns zeitnah mit einem konkreten Vorschlag.
          </p>
          <p class="hint">
            Wir verarbeiten Ihre Angaben vertraulich. Eine Kopie Ihrer Anfrage kann auf Wunsch bereitgestellt werden.
          </p>
        </form>

        <aside
          class="kontakt-card"
          :style="{ '--spot-x': `${spotlight.x}%`, '--spot-y': `${spotlight.y}%` }"
        >
          <div class="card-halo" aria-hidden="true" />
          <div class="card-header">
            <div class="badge">
              <span class="badge-icon">◎</span>
              <span>Kontaktieren Sie uns</span>
            </div>
            <p class="card-title">Wir steuern Ihre Bahndienstleistungen mit Präzision und Sorgfalt.</p>
            <p class="card-subtitle">Direkter Draht zu Disposition, Sicherheit & Einsatzleitung.</p>
          </div>

          <ul class="contact-list">
            <li>
              <span class="contact-icon" aria-hidden="true">📍</span>
              <div>
                <p class="contact-label">Standort Leitstelle</p>
                <p>Bahnhofsblick 12 · 31785 Hameln</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">✉️</span>
              <div>
                <p class="contact-label">E-Mail</p>
                <p>hello@babylon-bahndienste.de</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">☎️</span>
              <div>
                <p class="contact-label">Telefon</p>
                <p>+49 5161 301 700</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">🕒</span>
              <div>
                <p class="contact-label">Verfügbarkeit</p>
                <p>Disposition rund um die Uhr, Rückmeldung werktags <strong>&lt; 2 Std.</strong></p>
              </div>
            </li>
          </ul>

          <div class="cta-row">
            <div>
              <p class="micro">Lieber persönlich?</p>
              <p class="micro micro--strong">Wir vereinbaren sofort einen digitalen Kick-off.</p>
            </div>
            <a href="tel:+495161301700" class="card-cta">
              Direkt anrufen
              <span aria-hidden="true">→</span>
            </a>
          </div>
        </aside>
      </div>
    </section>

    <section class="assurance">
      <div class="assurance-card">
        <div class="assurance-beam" aria-hidden="true" />
        <div>
          <p class="eyebrow">Wie wir arbeiten</p>
          <h2>Klare Prozesse, dokumentierte Sicherheit, verlässliche Teams.</h2>
          <p class="lede">
            Von der Bedarfsaufnahme bis zur Einsatzdokumentation behalten Sie jederzeit den Überblick. Sie erhalten feste
            Ansprechpartner, verbindliche Zeitpläne und transparentes Reporting.
          </p>
        </div>
        <div class="assurance-grid" role="list">
          <div class="tile" role="listitem">
            <p class="tile-badge">01</p>
            <p class="tile-title">Briefing & Streckencheck</p>
            <p class="tile-copy">Analyse von Strecken, Baureihen und Sicherheitsauflagen für Ihren Auftrag.</p>
          </div>
          <div class="tile" role="listitem">
            <p class="tile-badge">02</p>
            <p class="tile-title">Einsatzsteuerung</p>
            <p class="tile-copy">Disposition mit redundanten Teams, klarer Schichtlogik und Slot-Management.</p>
          </div>
          <div class="tile" role="listitem">
            <p class="tile-badge">03</p>
            <p class="tile-title">Reporting</p>
            <p class="tile-copy">Statusmeldungen, Tagesreports und revisionssichere Dokumentation – digital bereitgestellt.</p>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<style scoped>
.kontakt-page {
  position: relative;
  isolation: isolate;
  display: flex;
  flex-direction: column;
  gap: 2.5rem;
}

.kontakt-grid {
  position: absolute;
  inset: 0;
  pointer-events: none;
  mask-image: radial-gradient(circle at 60% 40%, rgba(0, 0, 0, 0.55), transparent 70%);
}

.grid-line {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, rgba(249, 210, 112, 0.1), transparent 18%, transparent 82%, rgba(249, 210, 112, 0.08));
  background-size: 240px 1px;
  opacity: 0.45;
}

.grid-line--horizontal {
  background: linear-gradient(180deg, rgba(249, 210, 112, 0.12), transparent 14%, transparent 80%, rgba(249, 210, 112, 0.09));
  background-size: 1px 220px;
}

.kontakt-hero {
  position: relative;
  border: 1px solid rgba(249, 210, 112, 0.12);
  border-radius: 28px;
  padding: 2rem;
  background: radial-gradient(circle at 30% 20%, rgba(249, 210, 112, 0.08), transparent 28%),
    radial-gradient(circle at 90% 0%, rgba(100, 220, 255, 0.05), transparent 30%),
    rgba(10, 10, 12, 0.9);
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  overflow: hidden;
}

.hero-header {
  display: grid;
  gap: 0.65rem;
  max-width: 760px;
  margin-bottom: 1.3rem;
}

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 0.75rem;
  color: #f9d270;
  font-weight: 700;
}

h1 {
  margin: 0;
  font-size: clamp(2rem, 3vw + 1rem, 3rem);
  line-height: 1.15;
}

h2 {
  margin: 0;
  font-size: clamp(1.6rem, 1.3vw + 1rem, 2.2rem);
  line-height: 1.25;
}

.lede {
  color: #dbe8ff;
  max-width: 780px;
  margin: 0;
}

.signal-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.signal-chip {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.5rem 0.9rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(249, 210, 112, 0.14);
  color: #f7f1e7;
  font-weight: 600;
}

.pulse {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #f9d270;
  position: relative;
  box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.6);
  animation: pulse 2.4s ease-out infinite;
}

.pulse--cyan {
  background: #76e1ff;
  box-shadow: 0 0 0 0 rgba(118, 225, 255, 0.6);
}

.pulse--magenta {
  background: #ff8ad6;
  box-shadow: 0 0 0 0 rgba(255, 138, 214, 0.55);
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0.6);
  }
  70% {
    box-shadow: 0 0 0 16px rgba(249, 210, 112, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(249, 210, 112, 0);
  }
}

.kontakt-panels {
  display: grid;
  grid-template-columns: minmax(0, 1.2fr) minmax(320px, 0.8fr);
  gap: 1.4rem;
  margin-top: 0.5rem;
}

.kontakt-form {
  background: rgba(8, 8, 10, 0.9);
  border: 1px solid rgba(255, 255, 255, 0.03);
  border-radius: 24px;
  padding: 1.3rem;
  box-shadow: inset 0 0 0 1px rgba(249, 210, 112, 0.08), 0 16px 40px rgba(0, 0, 0, 0.4);
  display: grid;
  gap: 1rem;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.8rem;
}

.field {
  display: grid;
  gap: 0.4rem;
  color: #e6edff;
  font-weight: 600;
  font-size: 0.95rem;
}

.field span {
  color: #c7d7f7;
}

input,
select,
textarea {
  width: 100%;
  border-radius: 14px;
  border: 1px solid rgba(255, 255, 255, 0.06);
  padding: 0.9rem 1rem;
  background: rgba(255, 255, 255, 0.03);
  color: #fdfdfd;
  font-size: 1rem;
  transition: border-color 0.2s ease, box-shadow 0.2s ease, transform 0.2s ease;
  outline: none;
}

select {
  appearance: none;
  background-image: linear-gradient(135deg, transparent 50%, #f9d270 50%), linear-gradient(45deg, transparent 50%, #f9d270 50%);
  background-position: calc(100% - 18px) 55%, calc(100% - 12px) 55%;
  background-size: 8px 8px, 8px 8px;
  background-repeat: no-repeat;
}

textarea {
  resize: vertical;
  min-height: 140px;
}

input:focus,
select:focus,
textarea:focus {
  border-color: rgba(249, 210, 112, 0.7);
  box-shadow: 0 0 0 3px rgba(249, 210, 112, 0.18);
  transform: translateY(-1px);
}

.field--wide {
  grid-column: 1 / -1;
}

.form-actions {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.9rem;
}

.toggle {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  color: #dbe8ff;
  font-weight: 600;
  cursor: pointer;
  user-select: none;
}

.toggle input {
  display: none;
}

.toggle-slider {
  width: 52px;
  height: 28px;
  border-radius: 999px;
  background: linear-gradient(120deg, rgba(249, 210, 112, 0.75), rgba(201, 144, 56, 0.85));
  position: relative;
  box-shadow: 0 6px 18px rgba(249, 210, 112, 0.3);
}

.toggle-slider::after {
  content: '';
  position: absolute;
  top: 4px;
  left: 4px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #0a0a0c;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.45);
  transition: transform 0.2s ease;
}

.toggle input:checked + .toggle-slider::after {
  transform: translateX(24px);
}

.toggle-label {
  font-weight: 600;
}

.cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.95rem 1.3rem;
  border-radius: 14px;
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  font-weight: 800;
  font-size: 1rem;
  border: none;
  cursor: pointer;
  box-shadow: 0 18px 45px rgba(249, 210, 112, 0.35);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.cta:hover,
.cta:focus-visible {
  transform: translateY(-2px) scale(1.01);
  box-shadow: 0 22px 55px rgba(201, 144, 56, 0.38);
}

.cta-icon {
  font-size: 1.1rem;
}

.hint {
  margin: 0;
  color: #a8b9d8;
  font-size: 0.95rem;
}

.success {
  color: #b2f5b4;
  font-weight: 700;
}

.kontakt-card {
  position: relative;
  overflow: hidden;
  border-radius: 22px;
  padding: 1.4rem;
  background: radial-gradient(circle at var(--spot-x, 50%) var(--spot-y, 50%), rgba(249, 210, 112, 0.12), transparent 30%),
    linear-gradient(135deg, rgba(255, 255, 255, 0.03), rgba(0, 0, 0, 0.55)),
    #040405;
  border: 1px solid rgba(249, 210, 112, 0.18);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.6), inset 0 0 0 1px rgba(255, 255, 255, 0.04);
  display: grid;
  gap: 1rem;
}

.card-halo {
  position: absolute;
  inset: 12% 8%;
  background: radial-gradient(circle at 20% 20%, rgba(249, 210, 112, 0.08), transparent 40%),
    radial-gradient(circle at 80% 70%, rgba(118, 225, 255, 0.06), transparent 42%);
  filter: blur(10px);
  z-index: 0;
}

.card-header,
.contact-list,
.cta-row {
  position: relative;
  z-index: 1;
}

.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.55rem;
  padding: 0.45rem 0.85rem;
  background: rgba(249, 210, 112, 0.12);
  border-radius: 999px;
  border: 1px solid rgba(249, 210, 112, 0.28);
  color: #f9d270;
  font-weight: 700;
  letter-spacing: 0.03em;
  text-transform: uppercase;
}

.badge-icon {
  display: grid;
  place-items: center;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: rgba(249, 210, 112, 0.2);
  color: #0a0a0c;
}

.card-title {
  margin: 0.6rem 0 0.25rem;
  font-size: 1.4rem;
  line-height: 1.3;
  color: #fdfdfd;
}

.card-subtitle {
  margin: 0;
  color: #c8d6f0;
}

.contact-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.85rem;
}

.contact-list li {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.75rem;
  align-items: start;
  padding: 0.75rem 0.8rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.contact-icon {
  font-size: 1.1rem;
}

.contact-label {
  margin: 0;
  color: #f9d270;
  font-weight: 700;
}

.contact-list p {
  margin: 0;
  color: #e8f0ff;
}

.cta-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.8rem;
  padding: 0.9rem 1rem;
  border-radius: 16px;
  background: linear-gradient(90deg, rgba(249, 210, 112, 0.08), rgba(0, 0, 0, 0.4));
  border: 1px solid rgba(249, 210, 112, 0.3);
}

.micro {
  margin: 0;
  color: #dbe8ff;
  font-size: 0.95rem;
}

.micro--strong {
  color: #ffffff;
  font-weight: 700;
}

.card-cta {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.75rem 1rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.4);
  color: #f9d270;
  text-decoration: none;
  border: 1px solid rgba(249, 210, 112, 0.4);
  transition: transform 0.2s ease, border-color 0.2s ease, background 0.2s ease;
}

.card-cta:hover,
.card-cta:focus-visible {
  transform: translateY(-1px);
  border-color: rgba(249, 210, 112, 0.65);
  background: rgba(249, 210, 112, 0.08);
}

.assurance {
  position: relative;
}

.assurance-card {
  position: relative;
  padding: 2rem;
  border-radius: 24px;
  border: 1px solid rgba(249, 210, 112, 0.14);
  background: rgba(10, 10, 12, 0.88);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  display: grid;
  gap: 1.2rem;
}

.assurance-beam {
  position: absolute;
  inset: -30% 20% auto;
  height: 120%;
  background: linear-gradient(120deg, rgba(249, 210, 112, 0.18), rgba(118, 225, 255, 0));
  filter: blur(40px);
  transform: rotate(-4deg);
  opacity: 0.6;
  z-index: 0;
}

.assurance-card > * {
  position: relative;
  z-index: 1;
}

.assurance-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 1rem;
}

.tile {
  padding: 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.06);
  display: grid;
  gap: 0.4rem;
  position: relative;
  overflow: hidden;
}

.tile::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 20% 20%, rgba(249, 210, 112, 0.14), transparent 40%);
  opacity: 0;
  transition: opacity 0.2s ease;
}

.tile:hover::after,
.tile:focus-within::after {
  opacity: 1;
}

.tile-badge {
  margin: 0;
  color: #f9d270;
  font-weight: 700;
  letter-spacing: 0.06em;
}

.tile-title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 700;
}

.tile-copy {
  margin: 0;
  color: #c7d7f7;
}

@media (max-width: 1024px) {
  .kontakt-panels {
    grid-template-columns: 1fr;
  }

  .kontakt-card {
    order: -1;
  }
}

@media (max-width: 720px) {
  .form-grid {
    grid-template-columns: 1fr;
  }

  .kontakt-hero,
  .assurance-card {
    padding: 1.2rem;
  }
}
</style>
