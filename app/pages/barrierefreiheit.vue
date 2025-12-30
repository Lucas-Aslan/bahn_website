<script setup lang="ts">
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
</script>

<template>
  <div class="a11y-page">
    <section class="hero">
      <div class="hero__beam" aria-hidden="true" />
      <div class="hero__content">
        <p class="eyebrow">Barrierefreiheit</p>
        <h1>Erklärung zur digitalen Barrierefreiheit</h1>
        <p class="lede">
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
        <div class="panel__halo" aria-hidden="true" />
        <p class="panel__eyebrow">Was Sie erwartet</p>
        <p class="panel__title">Transparente Standards & kontinuierliche Verbesserung</p>
        <p class="panel__text">
          Unsere Seiten werden fortlaufend geprüft und an aktuelle Anforderungen angepasst. Hinweise und Verbesserungsvorschläge
          setzen wir – soweit möglich – kurzfristig um.
        </p>
        <div class="panel__tags" role="list">
          <span class="pill" role="listitem">Kontraststarke Gestaltung</span>
          <span class="pill" role="listitem">Klare Fokus-Reihenfolge</span>
          <span class="pill" role="listitem">Tastaturnavigation</span>
        </div>
      </div>
    </section>

    <section class="grid">
      <article class="card card--primary">
        <div class="card__head">
          <p class="eyebrow">Selbstverpflichtung</p>
          <h2>Rechtliche Grundlagen</h2>
          <p class="lede">
            Wir setzen alles daran, dass unsere Webinhalte ohne Barrieren nutzbar sind. Maßstab sind die Vorgaben des § 12d BGG
            sowie die Anforderungen der BITV 2.0.
          </p>
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

      <aside class="side">
        <div class="card card--glass">
          <div class="side__head">
            <p class="side__eyebrow">Kontakt für Feedback</p>
            <p class="side__title">Melden Sie Barrieren direkt an unser Team.</p>
          </div>
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

        <div class="card card--meta">
          <p class="side__eyebrow">Stand</p>
          <p class="side__title">Dezember 2025</p>
          <p class="micro">Diese Seite wird aktualisiert, sobald Prozesse oder Inhalte angepasst werden.</p>
        </div>
      </aside>
    </section>

    <section class="section">
      <div class="section__head">
        <p class="eyebrow">Aktuelle Einschränkungen</p>
        <h2>Welche Bereiche sind noch nicht barrierefrei?</h2>
        <p class="lede">
          Einzelne Inhalte erfüllen noch nicht vollständig die Kriterien der WCAG 2.1. Wir arbeiten an folgenden Punkten mit hoher Priorität.
        </p>
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

    <section class="mediation">
      <article class="card card--primary">
        <div class="card__head">
          <p class="eyebrow">Schlichtung</p>
          <h2>Hinweis zum Schlichtungsverfahren</h2>
          <p class="lede">
            Sollte Ihr Feedback nicht zu einem zufriedenstellenden Ergebnis führen, können Sie ein Schlichtungsverfahren nach § 16 BGG beantragen.
          </p>
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
  display: grid;
  gap: 2rem;
  padding: 0.5rem 0 2.5rem;
}

.hero {
  position: relative;
  display: grid;
  gap: 1.2rem;
  grid-template-columns: minmax(0, 1.2fr) minmax(320px, 0.8fr);
  align-items: stretch;
  border-radius: 26px;
  padding: clamp(1.4rem, 2vw, 2rem);
  background: radial-gradient(circle at 24% 24%, rgba(199, 117, 139, 0.12), transparent 38%),
    radial-gradient(circle at 80% 16%, rgba(0, 72, 49, 0.08), transparent 36%),
    linear-gradient(135deg, var(--color-paper), var(--color-cream));
  border: 1px solid rgba(199, 117, 139, 0.18);
  box-shadow: 0 28px 70px rgba(0, 0, 0, 0.12), inset 0 0 0 1px rgba(255, 255, 255, 0.6);
  overflow: hidden;
}

.hero__beam {
  position: absolute;
  inset: -60% 30% auto -40%;
  height: 120%;
  background: radial-gradient(circle, rgba(199, 117, 139, 0.18), transparent 42%);
  filter: blur(38px);
  opacity: 0.9;
  animation: float 9s ease-in-out infinite alternate;
  pointer-events: none;
}

.hero__content {
  position: relative;
  display: grid;
  gap: 0.9rem;
  z-index: 1;
}

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-size: 0.82rem;
  color: var(--color-rose);
  font-weight: 700;
}

h1 {
  margin: 0;
  font-size: clamp(2rem, 2vw + 1.2rem, 2.7rem);
  line-height: 1.15;
}

h2 {
  margin: 0;
  font-size: clamp(1.6rem, 1vw + 1.1rem, 2.1rem);
  line-height: 1.2;
}

.lede {
  margin: 0;
  color: #dbe5ff;
  max-width: 820px;
  line-height: 1.6;
}

.hero__meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  padding: 0.5rem 0.9rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(199, 117, 139, 0.14);
  color: #f7f2e6;
  font-weight: 600;
}

.chip--solid {
  background: linear-gradient(120deg, var(--color-rose), var(--color-forest));
  color: #ffffff;
  border: none;
  box-shadow: 0 12px 30px rgba(199, 117, 139, 0.3);
}

.hero__panel {
  position: relative;
  z-index: 1;
  padding: 1.4rem;
  border-radius: 20px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(199, 117, 139, 0.08), 0 16px 40px rgba(0, 0, 0, 0.4);
  display: grid;
  gap: 0.6rem;
}

.panel__halo {
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at 20% 20%, rgba(199, 117, 139, 0.15), transparent 36%),
    radial-gradient(circle at 80% 80%, rgba(255, 255, 255, 0.05), transparent 45%);
  filter: blur(12px);
  pointer-events: none;
}

.panel__eyebrow {
  margin: 0;
  color: #f6e6b4;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  font-weight: 700;
}

.panel__title {
  margin: 0;
  font-size: 1.2rem;
  font-weight: 800;
}

.panel__text {
  margin: 0;
  color: #d8e0f7;
}

.panel__tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.pill {
  display: inline-flex;
  align-items: center;
  padding: 0.45rem 0.75rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  color: #f2f4ff;
  font-weight: 600;
}

.grid {
  display: grid;
  gap: 1.2rem;
  grid-template-columns: minmax(0, 1.1fr) minmax(320px, 0.9fr);
}

.card {
  position: relative;
  border-radius: 22px;
  padding: 1.4rem;
  background: #ffffff;
  border: 1px solid rgba(0, 72, 49, 0.12);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.1), inset 0 0 0 1px rgba(255, 255, 255, 0.8);
}

.card--primary {
  background: radial-gradient(circle at 18% 14%, rgba(199, 117, 139, 0.08), transparent 34%),
    var(--color-paper);
  border-color: rgba(199, 117, 139, 0.16);
}

.card--glass {
  background: rgba(255, 255, 255, 0.9);
  border-color: rgba(0, 72, 49, 0.12);
}

.card--meta {
  background: rgba(255, 255, 255, 0.95);
  border-color: rgba(199, 117, 139, 0.12);
}

.card--note {
  background: var(--color-paper);
  border: 1px dashed rgba(199, 117, 139, 0.3);
}

.card__head {
  display: grid;
  gap: 0.4rem;
  margin-bottom: 0.6rem;
}

.card__body {
  display: grid;
  gap: 0.8rem;
  color: var(--color-muted);
}

.card__title {
  margin: 0 0 0.2rem;
  font-weight: 800;
}

.card__text {
  margin: 0;
  color: var(--color-muted);
}

.link-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.link-pill {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.5rem 0.85rem;
  border-radius: 999px;
  background: rgba(199, 117, 139, 0.14);
  color: #fefcf6;
  text-decoration: none;
  font-weight: 700;
  border: 1px solid rgba(199, 117, 139, 0.26);
  transition: transform 0.15s ease, box-shadow 0.2s ease, border-color 0.2s ease;
}

.link-pill:hover,
.link-pill:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 12px 30px rgba(199, 117, 139, 0.24);
  border-color: rgba(199, 117, 139, 0.4);
}

.link-pill--ghost {
  background: rgba(255, 255, 255, 0.04);
  border-color: rgba(255, 255, 255, 0.08);
  color: #f2f4ff;
}

.callout {
  margin-top: 0.3rem;
  padding: 0.9rem 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(199, 117, 139, 0.06);
}

.callout__label {
  margin: 0 0 0.25rem;
  font-weight: 700;
  color: var(--color-rose);
}

.callout__text {
  margin: 0;
  color: #dce7ff;
}

.side {
  display: grid;
  gap: 0.8rem;
}

.side__head {
  display: grid;
  gap: 0.25rem;
}

.side__eyebrow {
  margin: 0;
  text-transform: uppercase;
  letter-spacing: 0.12em;
  color: #f6e6b4;
  font-weight: 700;
  font-size: 0.9rem;
}

.side__title {
  margin: 0;
  font-size: 1.2rem;
  font-weight: 800;
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

.contact-icon {
  display: inline-flex;
  width: 36px;
  height: 36px;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  background: rgba(199, 117, 139, 0.15);
  color: var(--color-rose);
  font-size: 1.1rem;
}

.contact-label {
  margin: 0;
  color: #d9e5ff;
  font-weight: 700;
}

a {
  color: var(--color-rose);
  text-decoration: none;
  font-weight: 700;
}

a:hover,
a:focus-visible {
  text-decoration: underline;
}

.micro {
  margin: 0;
  color: #aeb8d5;
  font-size: 0.9rem;
  line-height: 1.4;
}

.section {
  display: grid;
  gap: 1rem;
}

.section__head {
  display: grid;
  gap: 0.35rem;
}

.tiles {
  display: grid;
  gap: 0.7rem;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
}

.tile {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.6rem;
  align-items: start;
  padding: 0.95rem 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(199, 117, 139, 0.05);
}

.tile__badge {
  width: 28px;
  height: 28px;
  border-radius: 999px;
  display: grid;
  place-items: center;
  background: linear-gradient(135deg, var(--color-rose), var(--color-forest));
  color: #ffffff;
  font-weight: 800;
}

.tile__title {
  margin: 0;
  font-weight: 800;
  color: #f7f2e6;
}

.tile__text {
  margin: 0.15rem 0 0;
  color: #cbd6f5;
}

.mediation {
  display: grid;
  gap: 0.8rem;
}

@keyframes float {
  0% {
    transform: translateY(-12px);
  }
  100% {
    transform: translateY(8px);
  }
}

@media (max-width: 980px) {
  .hero,
  .grid {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 640px) {
  .hero {
    padding: 1rem;
  }

  .card,
  .card--primary {
    padding: 1.1rem;
  }

  .hero__meta {
    flex-direction: column;
  }
}
</style>
