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
