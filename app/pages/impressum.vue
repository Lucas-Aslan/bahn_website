<script setup lang="ts">
const companyDetails = [
  { label: 'Firma', value: 'Babylon Bahndienste UG (haftungsbeschränkt)' },
  { label: 'Angaben gemäß § 5 DDG', value: 'Frankfurter Weg 27 · 33106 Paderborn' },
  { label: 'Vertreten durch', value: 'Geschäftsführer: Sanharip Aras' },
  { label: 'Handelsregister', value: 'Amtsgericht Bielefeld · HRB 123456' },
  { label: 'Umsatzsteuer-ID', value: 'DE123456789' }
]

const contactDetails = [
  { label: 'Telefon', value: '+49 123 456 789' },
  { label: 'E-Mail', value: 'info@babylon-bahndienste.de' },
]

const oversightDetails = [
  {
    label: 'Aufsichtsbehörde',
    value: 'Eisenbahn-Bundesamt (EBA), Heinemannstraße 6, 53175 Bonn'
  },
  {
    label: 'Online-Streitbeilegung',
    value: 'Plattform der EU-Kommission:',
    link: 'https://ec.europa.eu/consumers/odr',
    note: 'Unsere E-Mail-Adresse finden Sie oben im Impressum.'
  },
  {
    label: 'Verbraucherschlichtung',
    value: 'Wir sind nicht bereit oder verpflichtet, an Streitbeilegungsverfahren vor einer Verbraucherschlichtungsstelle teilzunehmen.'
  },
  {
    label: 'Berufshaftpflicht',
    value: 'Allianz Versicherungs-AG · Geltungsbereich: EU-Mitgliedsstaaten'
  }
]

const liabilityNotes = [
  {
    title: 'Haftung für Inhalte',
    text:
      'Als Diensteanbieter sind wir gemäß § 5 Abs. 1 DDG für eigene Inhalte nach den allgemeinen Gesetzen verantwortlich. Verpflichtungen zur Entfernung oder Sperrung der Nutzung von Informationen nach den allgemeinen Gesetzen bleiben hiervon unberührt. Eine Haftung ist erst ab dem Zeitpunkt der Kenntnis einer konkreten Rechtsverletzung möglich; bei Bekanntwerden werden wir entsprechende Inhalte umgehend entfernen.'
  },
  {
    title: 'Haftung für Links',
    text:
      'Unser Angebot enthält Links zu externen Websites Dritter, auf deren Inhalte wir keinen Einfluss haben. Für diese fremden Inhalte übernehmen wir keine Gewähr; verantwortlich sind die jeweiligen Anbieter. Die verlinkten Seiten wurden zum Zeitpunkt der Verlinkung auf mögliche Rechtsverstöße überprüft; rechtswidrige Inhalte waren nicht erkennbar. Bei Bekanntwerden von Rechtsverletzungen entfernen wir Links umgehend.'
  },
  {
    title: 'Urheberrecht',
    text:
      'Die durch den Seitenbetreiber erstellten Inhalte und Werke unterliegen dem deutschen Urheberrecht. Vervielfältigung, Bearbeitung, Verbreitung oder jede Art der Verwertung außerhalb der Grenzen des Urheberrechts bedürfen der vorherigen schriftlichen Zustimmung. Inhalte Dritter werden als solche gekennzeichnet; sollten Sie eine Urheberrechtsverletzung feststellen, informieren Sie uns bitte, damit wir die Inhalte umgehend entfernen.'
  }
]
</script>

<template>
  <div class="impressum-page">
    <section class="impressum-hero">
      <div class="hero-copy">
        <p class="eyebrow">Rechtliche Angaben</p>
        <h1>Impressum</h1>
        <p class="lede">
          Transparente Kontaktdaten, klare Verantwortlichkeiten und Aufsichtsangaben für Babylon Bahndienste. Alle
          Informationen auf einen Blick, aktuell gepflegt und jederzeit erreichbar.
        </p>

        <div class="hero-chips" role="list">
          <span class="chip" role="listitem">Verantwortlich nach § 5 DDG</span>
          <span class="chip" role="listitem">Schnelle Kontaktwege &amp; 24/7-Dispo</span>
        </div>
      </div>

      <div class="hero-panel" aria-label="Schnellkontakt">
        <div class="panel-halo" aria-hidden="true" />
        <div class="panel-head">
          <p class="panel-eyebrow">Kontakt</p>
          <p class="panel-title">Direkter Draht zur Leitstelle</p>
          <p class="panel-subtitle">Wir reagieren werktags innerhalb eines Werktags – in Einsatzfällen sofort.</p>
        </div>
        <ul class="panel-list">
          <li>
            <span class="icon" aria-hidden="true">☎️</span>
            <div>
              <p class="label">Telefon</p>
              <p class="value">+49 123 456 789</p>
            </div>
          </li>
          <li>
            <span class="icon" aria-hidden="true">✉️</span>
            <div>
              <p class="label">E-Mail</p>
              <p class="value">info@babylon-bahndienste.de</p>
            </div>
          </li>
          <li>
            <span class="icon" aria-hidden="true">📍</span>
            <div>
              <p class="label">Standort</p>
              <p class="value">Frankfurter Weg 27 · 33106 Paderborn</p>
            </div>
          </li>
        </ul>
        <div class="panel-foot">
          <p class="micro">Für eilbedürftige Einsätze ist unsere Disposition telefonisch rund um die Uhr erreichbar.</p>
          <NuxtLink to="/kontakt" class="panel-cta">Kontakt aufnehmen ↗</NuxtLink>
        </div>
      </div>
    </section>

    <section class="impressum-details">
      <div class="card">
        <div class="card-head">
          <p class="eyebrow">§ 5 DDG</p>
          <h2>Angaben zum Unternehmen</h2>
          <p class="lede">Rechtlich Verantwortliche und registrierte Angaben zu Babylon Bahndienste.</p>
        </div>
        <dl class="detail-list">
          <div v-for="item in companyDetails" :key="item.label" class="detail-row">
            <dt>{{ item.label }}</dt>
            <dd>{{ item.value }}</dd>
          </div>
        </dl>
      </div>

      <div class="card">
        <div class="card-head">
          <p class="eyebrow">Kommunikation</p>
          <h2>Kontakt &amp; Erreichbarkeit</h2>
          <p class="lede">Schnelle Rückmeldungen, abgestimmte Ansprechpartner und sichere Kanäle.</p>
        </div>
        <dl class="detail-list">
          <div v-for="item in contactDetails" :key="item.label" class="detail-row">
            <dt>{{ item.label }}</dt>
            <dd>{{ item.value }}</dd>
          </div>
        </dl>
      </div>
    </section>

    <section class="oversight">
      <div class="oversight-card">
        <div class="oversight-glow" aria-hidden="true" />
        <div class="oversight-head">
          <p class="eyebrow">Aufsicht &amp; Sicherheit</p>
          <h2>Regulatorische Hinweise</h2>
          <p class="lede">Zuständigkeiten, Versicherungsschutz und Hinweise zur Streitbeilegung.</p>
        </div>

        <div class="oversight-grid" role="list">
          <article v-for="item in oversightDetails" :key="item.label" class="oversight-tile" role="listitem">
            <p class="tile-label">{{ item.label }}</p>
            <p class="tile-value">
              <span>{{ item.value }}</span>
              <template v-if="item.link">
                <a :href="item.link" class="tile-link" rel="noopener noreferrer" target="_blank">
                  {{ item.link }}
                </a>
              </template>
              <span v-if="item.note" class="tile-note">{{ item.note }}</span>
            </p>
          </article>
        </div>
      </div>
    </section>

    <section class="liability">
      <div class="liability-head">
        <p class="eyebrow">Hinweise</p>
        <h2>Haftung &amp; Urheberrecht</h2>
        <p class="lede">Grundsätze zur Nutzung unserer Inhalte und externen Verlinkungen.</p>
      </div>

      <div class="liability-grid">
        <article v-for="note in liabilityNotes" :key="note.title" class="liability-card">
          <p class="liability-title">{{ note.title }}</p>
          <p class="liability-text">{{ note.text }}</p>
        </article>
      </div>

      <div class="liability-bottom">
        <p class="micro">
          Hinweise auf Rechtsverstöße oder fehlerhafte Inhalte können Sie jederzeit an
          <a href="mailto:info@babylon-bahndienste.de">info@babylon-bahndienste.de</a>
          richten. Wir prüfen Eingaben umgehend und aktualisieren betroffene Inhalte schnellstmöglich.
          Softwareunternehmen:
          <a href="https://www.eulah.de" target="_blank" rel="noopener noreferrer">www.eulah.de</a>
          · Fotos: Babylon Bahndienste.
        </p>
      </div>

    </section>
  </div>
</template>
