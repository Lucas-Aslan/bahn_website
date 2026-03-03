<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

type Detail = {
  label: string
  value: string
}

type Oversight = {
  title: string
  description: string
  link?: string
}

type LegalNote = {
  title: string
  text: string
}

const companyDetails: Detail[] = [
  { label: 'Firma', value: 'Babylon Bahndienste UG (haftungsbeschränkt)' },
  { label: 'Angaben gemäß § 5 DDG', value: 'Frankfurter Weg 27 · 33106 Paderborn' },
  { label: 'Vertreten durch', value: 'Geschäftsführer: Sanharip Aras' },
  { label: 'Handelsregister', value: 'Amtsgericht Paderborn · HRB 16943' },
  { label: 'Umsatzsteuer-ID', value: 'DE366907962' }
]

const contactDetails: Detail[] = [
  { label: 'Telefon', value: '+49 160 216 1223' },
  { label: 'E-Mail', value: 'info@babylon-bahndienste.de' },
  { label: 'Dispo', value: '24/7 für eilbedürftige Einsätze erreichbar' }
]

const oversightDetails: Oversight[] = [
  {
    title: 'Aufsichtsbehörde',
    description: 'Eisenbahn-Bundesamt (EBA), Heinemannstraße 6, 53175 Bonn'
  },
  {
    title: 'Online-Streitbeilegung',
    description: 'Plattform der EU-Kommission für Verbraucherstreitbeilegung.',
    link: 'https://ec.europa.eu/consumers/odr'
  },
  {
    title: 'Verbraucherschlichtung',
    description:
      'Wir sind nicht bereit oder verpflichtet, an Streitbeilegungsverfahren vor einer Verbraucherschlichtungsstelle teilzunehmen.'
  },
  {
    title: 'Berufshaftpflicht',
    description: 'Allianz Versicherungs-AG · Geltungsbereich: EU-Mitgliedsstaaten'
  }
]

const liabilityNotes: LegalNote[] = [
  {
    title: 'Haftung für Inhalte',
    text:
      'Als Diensteanbieter sind wir gemäß § 5 Abs. 1 DDG für eigene Inhalte nach den allgemeinen Gesetzen verantwortlich. Verpflichtungen zur Entfernung oder Sperrung von Informationen nach den allgemeinen Gesetzen bleiben hiervon unberührt.'
  },
  {
    title: 'Haftung für Links',
    text:
      'Unser Angebot enthält Links zu externen Websites Dritter. Für diese fremden Inhalte übernehmen wir keine Gewähr; verantwortlich sind die jeweiligen Anbieter der verlinkten Seiten.'
  },
  {
    title: 'Urheberrecht',
    text:
      'Die durch den Seitenbetreiber erstellten Inhalte und Werke unterliegen dem deutschen Urheberrecht. Bei Bekanntwerden von Rechtsverletzungen entfernen wir betroffene Inhalte umgehend.'
  }
]

let revealObserver: IntersectionObserver | null = null

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
  <div class="impressum-page">
    <section class="impressum-hero section js-reveal">
      <div class="impressum-hero__content">
        <p class="eyebrow">Rechtliche Angaben</p>
        <h1>Impressum</h1>
        <p class="section__lead">
          Transparente Kontaktdaten, klare Verantwortlichkeiten und regulatorische Hinweise zu Babylon Bahndienste –
          übersichtlich dargestellt im Stil unserer Karriereseite.
        </p>
        <div class="impressum-hero__actions">
          <a href="#angaben" class="cta cta--solid">Unternehmensangaben</a>
          <NuxtLink to="/kontakt" class="cta cta--ghost">Kontakt aufnehmen</NuxtLink>
        </div>
      </div>
      <div class="impressum-hero__image-wrap">
        <img src="/images/career-illustration.svg" alt="Babylon Bahndienste Impressum" class="impressum-hero__image" loading="lazy">
      </div>
    </section>

    <section id="angaben" class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">§ 5 DDG</p>
          <h2>Angaben zum Unternehmen</h2>
          <p class="section__lead">Rechtlich Verantwortliche und registrierte Unternehmensdaten.</p>
        </div>
      </div>
      <div class="detail-grid">
        <article v-for="item in companyDetails" :key="item.label" class="detail-card">
          <p class="detail-card__meta">{{ item.label }}</p>
          <h3>{{ item.value }}</h3>
        </article>
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header section__header--split">
        <div>
          <p class="eyebrow">Kommunikation</p>
          <h2>Kontakt &amp; Erreichbarkeit</h2>
          <p class="section__lead">Schnelle Rückmeldungen über abgestimmte Ansprechpartner und sichere Kanäle.</p>
        </div>
        <NuxtLink to="/kontakt" class="cta cta--solid">Jetzt Kontakt aufnehmen</NuxtLink>
      </div>

      <div class="detail-grid">
        <article v-for="item in contactDetails" :key="item.label" class="detail-card">
          <p class="detail-card__meta">{{ item.label }}</p>
          <h3>{{ item.value }}</h3>
        </article>
      </div>
    </section>

    <section class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Aufsicht &amp; Sicherheit</p>
          <h2>Regulatorische Hinweise</h2>
          <p class="section__lead">Zuständigkeiten, Versicherungen und Informationen zur Streitbeilegung.</p>
        </div>
      </div>
      <div class="detail-grid">
        <article v-for="item in oversightDetails" :key="item.title" class="detail-card">
          <p class="detail-card__meta">{{ item.title }}</p>
          <h3>{{ item.description }}</h3>
          <a v-if="item.link" :href="item.link" class="text-link" rel="noopener noreferrer" target="_blank">
            {{ item.link }}
          </a>
        </article>
      </div>
    </section>

    <section class="section section--cta js-reveal">
      <div>
        <p class="eyebrow">Haftung &amp; Urheberrecht</p>
        <h2>Rechtliche Hinweise</h2>
        <p class="section__lead">
          Hinweise zu Inhalten, externen Links und Nutzungsrechten. Bei Rechtsverstößen bitte an
          <a href="mailto:info@babylon-bahndienste.de">info@babylon-bahndienste.de</a> wenden.
        </p>
      </div>
      <div class="notes-list">
        <article v-for="note in liabilityNotes" :key="note.title" class="note-item">
          <p class="detail-card__meta">{{ note.title }}</p>
          <p>{{ note.text }}</p>
        </article>
      </div>
    </section>
  </div>
</template>

<style scoped>
.impressum-page {
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

.section__header--split {
  align-items: center;
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

.impressum-hero {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(199, 117, 139, 0.12), rgba(0, 72, 49, 0.08));
  border-radius: 24px;
}

.impressum-hero__content h1 {
  margin: 0.2rem 0 0.45rem;
  font-size: clamp(2rem, 3vw, 2.6rem);
  color: var(--color-forest);
}

.impressum-hero__actions {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  margin-top: 1rem;
}

.impressum-hero__image-wrap {
  border-radius: 18px;
  overflow: hidden;
  border: 1px solid var(--color-border);
  box-shadow: 0 20px 45px rgba(0, 0, 0, 0.1);
  background: white;
}

.impressum-hero__image {
  width: 100%;
  height: 100%;
  min-height: 260px;
  object-fit: cover;
  display: block;
}

.detail-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 230px), 1fr));
  gap: 1rem;
}

.detail-card,
.note-item {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: 18px;
  padding: 1rem;
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.06);
}

.detail-card h3 {
  margin: 0;
  color: var(--color-forest);
  font-size: 1.05rem;
  line-height: 1.4;
}

.detail-card__meta {
  margin: 0 0 0.45rem;
  font-size: 0.85rem;
  color: var(--color-rose);
  font-weight: 700;
}

.text-link {
  margin-top: 0.9rem;
  display: inline-flex;
  text-decoration: none;
  font-weight: 700;
  color: var(--color-forest);
  word-break: break-all;
}

.section--cta {
  display: grid;
  gap: 1rem;
  background: linear-gradient(135deg, rgba(0, 72, 49, 0.08), rgba(199, 117, 139, 0.12));
  border-radius: 24px;
}

.notes-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(100%, 240px), 1fr));
  gap: 1rem;
}

.note-item p {
  margin: 0;
  color: var(--color-muted);
  line-height: 1.55;
}

@media (max-width: 900px) {
  .impressum-hero {
    grid-template-columns: 1fr;
  }
}
</style>
