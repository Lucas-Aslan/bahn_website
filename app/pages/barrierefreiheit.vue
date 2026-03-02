<script setup lang="ts">
import { onBeforeUnmount, onMounted } from 'vue'

const regulationLinks = [
  { label: 'Behindertengleichstellungsgesetz (BGG)', href: 'https://www.gesetze-im-internet.de/bgg/' },
  { label: 'Barrierefreie-Informationstechnik-Verordnung (BITV 2.0)', href: 'https://www.gesetze-im-internet.de/bitv_2_0/' },
  { label: 'EU-Richtlinie 2016/2102', href: 'https://eur-lex.europa.eu/eli/dir/2016/2102/oj' }
]

const partialAreas = [
  {
    title: 'Ältere Videos',
    detail:
      'Bei älteren Videoinhalten können Untertitel oder Audiodeskription noch fehlen. Wir liefern diese nach, sobald Produktionsfenster frei sind.'
  },
  {
    title: 'Externe Inhalte',
    detail:
      'Einbindungen von Drittanbietern (z. B. Karten, Bewerbungsportale) können Barrieren enthalten, die außerhalb unseres direkten Einflusses liegen.'
  },
  {
    title: 'PDF-Downloads im Umbau',
    detail:
      'Ältere PDF-Dokumente erfüllen noch nicht überall die PDF/UA-Kriterien. Wir überführen sie schrittweise in barrierearme Formate.'
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
  <div class="a11y-page">
    <section class="hero section js-reveal">
      <div class="hero__content">
        <p class="eyebrow">Barrierefreiheit</p>
        <h1>Erklärung zur digitalen Barrierefreiheit</h1>
        <p class="section__lead">
          Informationen zu unserem barrierefreien Webauftritt – inklusive rechtlicher Grundlagen, aktuellem Status und
          Kontaktwegen für Feedback.
        </p>

        <div class="hero__meta" role="list">
          <span class="chip chip--solid" role="listitem">Ausrichtung: WCAG 2.1 Level AA</span>
          <span class="chip" role="listitem">Selbstbewertung: Dezember 2025</span>
          <span class="chip" role="listitem">Letztes Update: Januar 2026</span>
        </div>
      </div>

      <div class="hero__panel" aria-label="Kurzüberblick zur Barrierefreiheit">
        <p class="hero__panel-eyebrow">Was Sie erwartet</p>
        <p class="hero__panel-title">Transparente Standards & kontinuierliche Verbesserung</p>
        <p class="section__lead">
          Unsere Seiten werden fortlaufend geprüft und an aktuelle Anforderungen angepasst. Hinweise und Verbesserungsvorschläge
          setzen wir – soweit möglich – kurzfristig um.
        </p>
        <div class="hero__tags" role="list">
          <span class="pill" role="listitem">Kontraststarke Gestaltung</span>
          <span class="pill" role="listitem">Klare Fokus-Reihenfolge</span>
          <span class="pill" role="listitem">Tastaturnavigation</span>
        </div>
      </div>
    </section>

    <section class="content-grid js-reveal">
      <article class="card card--primary">
        <div class="section__header">
          <div>
            <p class="eyebrow">Selbstverpflichtung</p>
            <h2>Rechtliche Grundlagen</h2>
            <p class="section__lead">
              Wir setzen alles daran, dass unsere Webinhalte ohne Barrieren nutzbar sind. Maßstab sind die Vorgaben des § 12d BGG
              sowie die Anforderungen der BITV 2.0.
            </p>
          </div>
        </div>

        <div class="card__body">
          <p>
            Babylon Bahndienste entwickelt Inhalte so, dass sie mit Screenreadern, Tastatur und adaptiven Technologien
            zugänglich sind. Unsere Prozesse orientieren sich an den Prinzipien wahrnehmbar, bedienbar, verständlich und robust.
          </p>
          <div class="link-pills" role="list">
            <a
              v-for="link in regulationLinks"
              :key="link.label"
              :href="link.href"
              class="link-pill"
              rel="noopener noreferrer"
              target="_blank"
              role="listitem"
            >
              {{ link.label }}
            </a>
            <span class="link-pill link-pill--ghost" role="listitem">WCAG 2.1 (Level AA)</span>
          </div>
          <div class="callout" role="note">
            <p class="callout__label">Status der Selbstbewertung</p>
            <p class="callout__text">
              Die letzte umfassende Prüfung erfolgte im Dezember 2025. Im Anschluss wurden Kontraste, Fokus-Stati und Formularhinweise
              aktualisiert; weitere Optimierungen laufen kontinuierlich.
            </p>
          </div>
        </div>
      </article>

      <aside class="side-stack">
        <div class="card">
          <p class="eyebrow">Kontakt für Feedback</p>
          <h3>Melden Sie Barrieren direkt an unser Team.</h3>
          <ul class="contact-list">
            <li>
              <span class="contact-icon" aria-hidden="true">✉️</span>
              <div>
                <p class="contact-label">E-Mail</p>
                <a href="mailto:info@babylon-bahndienste.de">info@babylon-bahndienste.de</a>
              </div>
            </li>
            <li>
              <span class="contact-icon" aria-hidden="true">☎️</span>
              <div>
                <p class="contact-label">Telefon</p>
                <a href="tel:+49123456789">+49 123 456 789</a>
              </div>
            </li>
          </ul>
          <p class="micro">
            Wir bestätigen eingehende Hinweise in der Regel am selben Werktag und priorisieren kritische Barrieren im nächsten Release.
          </p>
        </div>

        <div class="card">
          <p class="eyebrow">Stand</p>
          <h3>Dezember 2025</h3>
          <p class="micro">Diese Seite wird aktualisiert, sobald Prozesse oder Inhalte angepasst werden.</p>
        </div>
      </aside>
    </section>

    <section class="section js-reveal">
      <div class="section__header">
        <div>
          <p class="eyebrow">Aktuelle Einschränkungen</p>
          <h2>Welche Bereiche sind noch nicht barrierefrei?</h2>
          <p class="section__lead">
            Einzelne Inhalte erfüllen noch nicht vollständig die Kriterien der WCAG 2.1. Wir arbeiten an folgenden Punkten mit hoher Priorität.
          </p>
        </div>
      </div>

      <div class="tiles">
        <article v-for="area in partialAreas" :key="area.title" class="tile">
          <div class="tile__badge" aria-hidden="true">•</div>
          <div>
            <p class="tile__title">{{ area.title }}</p>
            <p class="tile__text">{{ area.detail }}</p>
          </div>
        </article>
      </div>

      <div class="card card--note" role="note">
        <p class="card__title">Unser Verbesserungsprozess</p>
        <p class="card__text">
          Wir priorisieren Hinweise aus Nutzertests und Audits. Neue Inhalte werden nach WCAG-Checklisten erstellt, bestehende
          Dokumente und Medien nach und nach auf barrierefreie Alternativen umgestellt.
        </p>
      </div>
    </section>

    <section class="section js-reveal">
      <article class="card card--primary">
        <div class="section__header">
          <div>
            <p class="eyebrow">Schlichtung</p>
            <h2>Hinweis zum Schlichtungsverfahren</h2>
            <p class="section__lead">
              Sollte Ihr Feedback nicht zu einem zufriedenstellenden Ergebnis führen, können Sie ein Schlichtungsverfahren nach § 16 BGG beantragen.
            </p>
          </div>
        </div>
        <div class="card__body">
          <p>
            Die Schlichtungsstelle BGG unterstützt dabei, Konflikte zur Barrierefreiheit zwischen Menschen mit Behinderungen und öffentlichen
            Stellen außergerichtlich zu lösen. Das Verfahren ist kostenlos und kann ohne Rechtsbeistand durchgeführt werden.
          </p>
          <div class="link-pills" role="list">
            <a
              href="https://www.schlichtungsstelle-bgg.de"
              class="link-pill"
              target="_blank"
              rel="noopener noreferrer"
              role="listitem"
            >
              schlichtungsstelle-bgg.de
            </a>
            <span class="pill" role="listitem">Kostenlos</span>
            <span class="pill" role="listitem">Ohne Rechtsbeistand</span>
            <span class="pill" role="listitem">Außergerichtlich</span>
          </div>
        </div>
      </article>
    </section>
  </div>
</template>

<style scoped>
.a11y-page {
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
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1.4rem;
  align-items: end;
  margin-bottom: 1rem;
}

h1 {
  margin: 0.2rem 0 0.45rem;
  font-size: clamp(2rem, 3vw, 2.6rem);
  color: var(--color-forest);
}

h2 {
  margin: 0.2rem 0 0.35rem;
  font-size: clamp(1.8rem, 3vw, 2.3rem);
  letter-spacing: -0.01em;
  color: var(--color-forest);
}

h3 {
  margin: 0.2rem 0 0.35rem;
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

.hero {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 1.5rem;
  align-items: center;
  background: linear-gradient(135deg, rgba(199, 117, 139, 0.12), rgba(0, 72, 49, 0.08));
  border-radius: 24px;
}

.hero__content {
  display: grid;
  gap: 0.9rem;
}

.hero__meta,
.hero__tags,
.link-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.hero__panel,
.card,
.tile {
  background: #fff;
  border: 1px solid var(--color-border);
  border-radius: 18px;
  padding: 1rem;
  box-shadow: 0 14px 35px rgba(0, 0, 0, 0.06);
}

.hero__panel-eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: var(--color-rose);
  font-size: 0.82rem;
  font-weight: 700;
}

.hero__panel-title {
  margin: 0.35rem 0;
  font-size: 1.1rem;
  color: var(--color-forest);
  font-weight: 700;
}

.content-grid {
  display: grid;
  gap: 1.2rem;
  grid-template-columns: minmax(0, 1.1fr) minmax(300px, 0.9fr);
}

.card__body {
  display: grid;
  gap: 0.9rem;
  color: var(--color-muted);
}

.chip,
.pill {
  display: inline-flex;
  align-items: center;
  padding: 0.45rem 0.75rem;
  border-radius: 999px;
  background: #ffffff;
  border: 1px solid var(--color-border);
  color: var(--color-forest);
  font-weight: 600;
}

.chip--solid {
  background: var(--color-rose);
  color: #ffffff;
  border-color: transparent;
}

.link-pill {
  display: inline-flex;
  align-items: center;
  padding: 0.5rem 0.85rem;
  border-radius: 999px;
  background: rgba(199, 117, 139, 0.12);
  color: var(--color-forest);
  text-decoration: none;
  font-weight: 700;
  border: 1px solid rgba(199, 117, 139, 0.26);
}

.link-pill--ghost {
  background: #fff;
}

.callout,
.card--note {
  padding: 0.9rem 1rem;
  border-radius: 16px;
  background: rgba(199, 117, 139, 0.08);
  border: 1px solid rgba(199, 117, 139, 0.2);
}

.callout__label,
.card__title,
.tile__title,
.contact-label {
  margin: 0;
  font-weight: 700;
  color: var(--color-forest);
}

.callout__text,
.card__text,
.tile__text,
.micro {
  margin: 0.2rem 0 0;
  color: var(--color-muted);
  line-height: 1.55;
}

.side-stack {
  display: grid;
  gap: 0.8rem;
}

.contact-list {
  list-style: none;
  padding: 0;
  margin: 0.8rem 0;
  display: grid;
  gap: 0.6rem;
}

.contact-list li {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.6rem;
  align-items: center;
}

.contact-icon,
.tile__badge {
  width: 32px;
  height: 32px;
  border-radius: 999px;
  display: grid;
  place-items: center;
  background: rgba(199, 117, 139, 0.16);
}

a {
  color: var(--color-forest);
  font-weight: 700;
}

.tiles {
  display: grid;
  gap: 0.7rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
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

@media (max-width: 980px) {
  .hero,
  .content-grid {
    grid-template-columns: 1fr;
  }
}
</style>
