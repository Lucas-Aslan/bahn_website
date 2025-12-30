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
