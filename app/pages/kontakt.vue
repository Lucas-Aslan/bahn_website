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
        <div class="title-row">
          <h1>Gemeinsam fahren wir Ihre Projekte sicher ins Ziel.</h1>
          <span class="title-photo" aria-hidden="true" />
        </div>
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
              <input name="firstName" type="text" placeholder="Vorname" autocomplete="given-name">
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
              <input name="phone" type="tel" placeholder="+49 123 456 789" autocomplete="tel" required>
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
            <div class="card-photo" aria-hidden="true" />
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
                <p>Frankfurter Weg 27 · 33106 Paderborn</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">✉️</span>
              <div>
                <p class="contact-label">E-Mail</p>
                <p>info@babylon-bahndienste.de</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">☎️</span>
              <div>
                <p class="contact-label">Telefon</p>
                <p>+49 123 456 789</p>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">🕒</span>
              <div>
                <p class="contact-label">Verfügbarkeit</p>
                <p>Disposition rund um die Uhr!</p>
              </div>
            </li>
          </ul>
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

.title-row {
  display: inline-flex;
  align-items: center;
  gap: 0.8rem;
  flex-wrap: wrap;
}

.title-photo {
  width: clamp(120px, 12vw, 150px);
  aspect-ratio: 4 / 3;
  border-radius: 18px;
  background:
    linear-gradient(145deg, rgba(249, 210, 112, 0.4), rgba(201, 144, 56, 0.4)),
    url("data:image/svg+xml,%3Csvg width='400' height='300' viewBox='0 0 400 300' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cdefs%3E%3ClinearGradient id='a' x1='40' y1='20' x2='360' y2='280' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23F9D270'/%3E%3Cstop offset='1' stop-color='%23525B7A'/%3E%3C/linearGradient%3E%3ClinearGradient id='b' x1='0' y1='0' x2='0' y2='300' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23101014'/%3E%3Cstop offset='1' stop-color='%2307070A'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='400' height='300' rx='26' fill='url(%23b)'/%3E%3Cpath d='M40 220H360' stroke='url(%23a)' stroke-width='14' stroke-linecap='round' stroke-dasharray='10 18' opacity='0.7'/%3E%3Cpath d='M60 190H340' stroke='%23F9D270' stroke-width='6' stroke-linecap='round' stroke-dasharray='6 12' opacity='0.35'/%3E%3Cpath d='M120 160C120 142.327 134.327 128 152 128H248C265.673 128 280 142.327 280 160V190H120V160Z' fill='url(%23a)' opacity='0.85'/%3E%3Crect x='148' y='144' width='104' height='42' rx='10' fill='%23040507' opacity='0.55'/%3E%3Crect x='160' y='152' width='22' height='26' rx='6' fill='%23F9D270'/%3E%3Crect x='190' y='152' width='22' height='26' rx='6' fill='%23F9D270' opacity='0.8'/%3E%3Crect x='220' y='152' width='22' height='26' rx='6' fill='%23F9D270' opacity='0.65'/%3E%3Ccircle cx='200' cy='210' r='26' fill='%23040507' stroke='%23F9D270' stroke-width='4'/%3E%3Ccircle cx='200' cy='210' r='10' fill='%23F9D270'/%3E%3Ccircle cx='138' cy='210' r='20' fill='%23040507' stroke='%23F9D270' stroke-width='4' opacity='0.7'/%3E%3Ccircle cx='262' cy='210' r='20' fill='%23040507' stroke='%23F9D270' stroke-width='4' opacity='0.7'/%3E%3Ccircle cx='90' cy='80' r='18' fill='%23F9D270' opacity='0.4'/%3E%3Cpath d='M310 90C310 90 322 82 340 82C358 82 368 90 368 90' stroke='%23F9D270' stroke-width='5' stroke-linecap='round' opacity='0.6'/%3E%3Ccircle cx='330' cy='70' r='10' fill='%23F9D270' opacity='0.55'/%3E%3C/svg%3E");
  background-size: cover;
  background-position: center;
  border: 1px solid rgba(249, 210, 112, 0.26);
  box-shadow:
    0 12px 30px rgba(0, 0, 0, 0.45),
    0 0 0 1px rgba(255, 255, 255, 0.04);
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
.card-photo,
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

.card-photo {
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 16px;
  margin-bottom: 0.8rem;
  background:
    radial-gradient(circle at 20% 20%, rgba(249, 210, 112, 0.18), transparent 45%),
    url("data:image/svg+xml,%3Csvg width='640' height='360' viewBox='0 0 640 360' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cdefs%3E%3ClinearGradient id='c' x1='40' y1='40' x2='600' y2='320' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23F9D270'/%3E%3Cstop offset='1' stop-color='%23454D6D'/%3E%3C/linearGradient%3E%3ClinearGradient id='d' x1='0' y1='0' x2='0' y2='360' gradientUnits='userSpaceOnUse'%3E%3Cstop stop-color='%23101014'/%3E%3Cstop offset='1' stop-color='%23050608'/%3E%3C/linearGradient%3E%3C/defs%3E%3Crect width='640' height='360' rx='26' fill='url(%23d)'/%3E%3Crect x='180' y='92' width='280' height='140' rx='22' fill='url(%23c)' opacity='0.9'/%3E%3Crect x='208' y='120' width='224' height='84' rx='16' fill='%23040507' opacity='0.55'/%3E%3Crect x='224' y='136' width='44' height='52' rx='10' fill='%23F9D270'/%3E%3Crect x='280' y='136' width='44' height='52' rx='10' fill='%23F9D270' opacity='0.85'/%3E%3Crect x='336' y='136' width='44' height='52' rx='10' fill='%23F9D270' opacity='0.7'/%3E%3Cpath d='M150 246H490' stroke='url(%23c)' stroke-width='18' stroke-linecap='round' stroke-dasharray='12 22' opacity='0.75'/%3E%3Ccircle cx='252' cy='270' r='34' fill='%23040507' stroke='%23F9D270' stroke-width='6'/%3E%3Ccircle cx='252' cy='270' r='12' fill='%23F9D270'/%3E%3Ccircle cx='182' cy='270' r='26' fill='%23040507' stroke='%23F9D270' stroke-width='6' opacity='0.7'/%3E%3Ccircle cx='322' cy='270' r='26' fill='%23040507' stroke='%23F9D270' stroke-width='6' opacity='0.7'/%3E%3Ccircle cx='462' cy='110' r='18' fill='%23F9D270' opacity='0.45'/%3E%3Cpath d='M100 120C100 120 124 108 156 108C188 108 206 120 206 120' stroke='%23F9D270' stroke-width='6' stroke-linecap='round' opacity='0.65'/%3E%3Ccircle cx='136' cy='94' r='12' fill='%23F9D270' opacity='0.55'/%3E%3C/svg%3E");
  background-size: cover;
  background-position: center;
  border: 1px solid rgba(249, 210, 112, 0.2);
  box-shadow:
    0 14px 36px rgba(0, 0, 0, 0.55),
    0 0 0 1px rgba(255, 255, 255, 0.04);
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
