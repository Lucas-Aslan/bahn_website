<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref } from 'vue'

const services = [
  'Leistungsdisposition & Einsatzsteuerung',
  'Triebfahrzeugführer & Rangierpersonal',
  'Gleisbau & Infrastruktur-Begleitung',
  'Terminal- & Hafenlogistik',
  'Sicherheitskonzepte & Audits',
  'Beratung & Projektstart'
]

const submitted = ref(false)
const isSubmitting = ref(false)
const submitError = ref('')
let revealObserver: IntersectionObserver | null = null

const handleSubmit = async (event: Event) => {
  event.preventDefault()

  const form = event.target as HTMLFormElement | null
  if (!form || isSubmitting.value) {
    return
  }

  submitted.value = false
  submitError.value = ''
  isSubmitting.value = true

  try {
    const formData = new FormData(form)
    const response = await fetch('https://formsubmit.co/ajax/info@babylon-bahndienste.de', {
      method: 'POST',
      headers: {
        Accept: 'application/json'
      },
      body: formData
    })

    if (!response.ok) {
      throw new Error('Nachricht konnte nicht gesendet werden.')
    }

    submitted.value = true
    form.reset()
    window.setTimeout(() => {
      submitted.value = false
    }, 4200)
  }
  catch {
    submitError.value = 'Beim Senden ist ein Fehler aufgetreten. Bitte versuchen Sie es erneut.'
  }
  finally {
    isSubmitting.value = false
  }
}

onMounted(() => {
  const revealables = Array.from(document.querySelectorAll<HTMLElement>('.js-reveal'))
  revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('is-visible')
          revealObserver?.unobserve(entry.target)
        }
      })
    },
    {
      threshold: 0.2,
      rootMargin: '0px 0px -10% 0px'
    }
  )

  revealables.forEach((element, index) => {
    element.style.setProperty('--reveal-delay', `${index * 70}ms`)
    revealObserver?.observe(element)
  })
})

onBeforeUnmount(() => {
  revealObserver?.disconnect()
})
</script>

<template>
  <div class="contact-page">
    <section class="contact-hero section js-reveal">
      <div class="contact-hero__content">
        <p class="eyebrow">Kontakt</p>
        <h1>Gemeinsam fahren wir Ihr Projekt sicher ins Ziel.</h1>
        <p class="section__lead">
          Präzise Bahndienstleistungen, klare Absprachen und schnelle Reaktionszeiten. Teilen Sie uns Ihr Vorhaben mit –
          wir melden uns zeitnah mit einem konkreten Vorschlag.
        </p>
        <div class="contact-hero__actions">
          <a href="#kontaktformular" class="cta cta--solid">Anfrage senden</a>
          <NuxtLink to="/karriere" class="cta cta--ghost">Zur Karriereseite</NuxtLink>
        </div>
      </div>
      <div class="contact-hero__image-wrap">
        <img src="/images/cta-bild.jpg" alt="Babylon Bahndienste Kontakt" class="contact-hero__image" loading="lazy">
      </div>
    </section>

    <section id="kontaktformular" class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Kontaktformular</p>
          <h2>Direkter Draht zu Disposition & Einsatzleitung</h2>
          <p class="section__lead">
            Nutzen Sie das Formular für Anfragen zu Personal, Einsatzsteuerung und Projekten. Wir antworten verlässlich
            und strukturiert.
          </p>
        </div>
      </div>

      <div class="contact-grid">
        <form class="contact-form" @submit="handleSubmit">
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
            <!-- <label class="field">
              <span>Leistung *</span>
              <select name="service" required>
                <option value="">Leistung auswählen</option>
                <option v-for="service in services" :key="service" :value="service">{{ service }}</option>
              </select>
            </label> -->
          </div>

          <label class="field field--wide">
            <span>Nachricht</span>
            <textarea
              name="message"
              rows="4"
              placeholder="Beschreiben Sie Ihr Vorhaben, Zeitplan und Einsatzort."
              required
            />
          </label>

          <input type="hidden" name="_subject" value="Neue Kontaktanfrage über die Website">
          <input type="hidden" name="_template" value="table">
          <input type="hidden" name="_captcha" value="false">

          <div class="form-actions">
            <button type="submit" class="cta cta--solid" :disabled="isSubmitting">
              {{ isSubmitting ? 'Wird gesendet ...' : (submitted ? 'Nachricht gesendet' : 'Abschicken') }}
            </button>
          </div>

          <p v-if="submitted" class="hint success">Vielen Dank! Wir melden uns zeitnah mit einem konkreten Vorschlag.</p>
          <p v-if="submitError" class="hint error">{{ submitError }}</p>
          <p class="hint">Wir verarbeiten Ihre Angaben vertraulich und ausschließlich zur Kontaktaufnahme.</p>
        </form>

        <aside class="contact-card">
          <p class="job-card__meta">Babylon Bahndienste</p>
          <h3>Kontaktinformationen</h3>
          <ul class="contact-list">
            <li><strong>Standort:</strong> Frankfurter Weg 27 · 33106 Paderborn</li>
            <li><strong>E-Mail:</strong> info@babylon-bahndienste.de</li>
            <li><strong>Telefon:</strong> +49 160 216 1223</li>
            <li><strong>Verfügbarkeit:</strong> Disposition rund um die Uhr</li>
          </ul>
          <NuxtLink to="/" class="text-link">Zur Startseite →</NuxtLink>
        </aside>
      </div>
    </section>
  </div>
</template>

<style scoped>
.contact-page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.section {
  background: transparent;
  border-radius: 24px;
  padding: clamp(1.5rem, 2vw, 2rem);
}

.section__header {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 260px), 1fr));
  gap: 1.4rem;
  align-items: end;
  margin-bottom: 1rem;
}

h2 {
  margin: 0.2rem 0 0.35rem;
  font-size: clamp(1.8rem, 3vw, 2.3rem);
  letter-spacing: -0.01em;
  color: var(--color-forest);
}

.section__lead {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.6;
}

.eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--color-rose);
  font-size: 0.82rem;
  background: rgba(199, 117, 139, 0.12);
  padding: 0.3rem 0.75rem;
  border-radius: 999px;
  display: inline-flex;
}

.cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.85rem 1.2rem;
  border-radius: 12px;
  font-weight: 700;
  letter-spacing: 0.01em;
  text-decoration: none;
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
  border: 1px solid transparent;
  cursor: pointer;
}

.cta--solid {
  background: var(--color-rose);
  color: #ffffff;
  box-shadow: 0 18px 45px rgba(199, 117, 139, 0.28);
}

.cta--ghost {
  background: #ffffff;
  color: var(--color-forest);
  border-color: var(--color-border);
}

.cta:hover,
.cta:focus-visible {
  transform: translateY(-1px);
}

.cta:disabled {
  opacity: 0.7;
  cursor: wait;
  transform: none;
}

.js-reveal {
  opacity: 0;
  transform: translateY(24px);
  transition: opacity 0.6s ease, transform 0.6s ease;
  transition-delay: var(--reveal-delay, 0ms);
}

.js-reveal.is-visible {
  opacity: 1;
  transform: translateY(0);
}

.contact-hero {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(199, 117, 139, 0.12), rgba(0, 72, 49, 0.08));
  border-radius: 24px;
}

.contact-hero__content h1 {
  margin: 0.2rem 0 0.45rem;
  font-size: clamp(2rem, 3vw, 2.6rem);
  color: var(--color-forest);
}

.contact-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1rem;
}

.contact-hero__image-wrap {
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid var(--color-border);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.1);
}

.contact-hero__image {
  width: 100%;
  height: 100%;
  min-height: 260px;
  object-fit: cover;
  display: block;
}

.contact-grid {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 1rem;
}

.contact-form,
.contact-card {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: 18px;
  padding: 1rem;
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.06);
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 0.75rem;
}

.field {
  display: grid;
  gap: 0.35rem;
  font-size: 0.92rem;
  color: var(--color-muted);
}

.field--wide {
  margin-top: 0.75rem;
}

input,
select,
textarea {
  width: 100%;
  border: 1px solid var(--color-border);
  border-radius: 12px;
  padding: 0.75rem 0.8rem;
  font: inherit;
}

textarea {
  resize: vertical;
}

.form-actions {
  margin-top: 0.9rem;
}

.hint {
  margin: 0.65rem 0 0;
  color: var(--color-muted);
  font-size: 0.92rem;
}

.success {
  color: var(--color-forest);
  font-weight: 700;
}

.error {
  color: #b3261e;
  font-weight: 700;
}

.job-card__meta {
  margin: 0;
  font-size: 0.85rem;
  color: var(--color-rose);
  font-weight: 700;
}

.contact-card h3 {
  margin: 0.4rem 0;
  color: var(--color-forest);
}

.contact-list {
  margin: 0;
  padding-left: 1rem;
  color: var(--color-muted);
  display: grid;
  gap: 0.55rem;
}

.text-link {
  margin-top: 0.9rem;
  display: inline-flex;
  text-decoration: none;
  font-weight: 700;
  color: var(--color-forest);
}

@media (max-width: 900px) {
  .contact-hero,
  .contact-grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 620px) {
  .form-grid {
    grid-template-columns: 1fr;
  }
}
</style>
