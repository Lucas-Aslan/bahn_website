<script setup lang="ts">
const companyDetails = [
  { label: 'Firma', value: 'Babylon Bahndienste UG (haftungsbeschränkt)' },
  { label: 'Angaben gemäß § 5 DDG', value: 'Frankfurter Weg 27 · 33106 Paderborn' },
  { label: 'Vertreten durch', value: 'Geschäftsführer: Marlon Becker' },
  { label: 'Handelsregister', value: 'Amtsgericht Bielefeld · HRB 123456' },
  { label: 'Umsatzsteuer-ID', value: 'DE123456789' }
]

const contactDetails = [
  { label: 'Telefon', value: '+49 123 456 789' },
  { label: 'Telefax', value: 'Derzeit nicht im Einsatz' },
  { label: 'E-Mail', value: 'info@babylon-bahndienste.de' },
  { label: 'Ansprechpartner Rechtliches', value: 'legal@babylon-bahndienste.de' }
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
          Hinweise auf Rechtsverstöße oder fehlerhafte Inhalte können Sie jederzeit an legal@babylon-bahndienste.de
          richten. Wir prüfen Eingaben umgehend und aktualisieren betroffene Inhalte schnellstmöglich. Softwareunternehmen:
          www.eulah.de · Fotos: Babylon Bahndienste.
        </p>
      </div>
    </section>
  </div>
</template>

<style scoped>
.impressum-page {
  position: relative;
  display: grid;
  gap: 2rem;
  padding: 1rem 0 2rem;
}

.impressum-hero {
  position: relative;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.4rem;
  padding: 1.5rem;
  border-radius: 26px;
  background: radial-gradient(circle at 12% 18%, rgba(249, 210, 112, 0.1), transparent 32%),
    radial-gradient(circle at 82% 24%, rgba(118, 225, 255, 0.08), transparent 36%),
    rgba(8, 8, 10, 0.9);
  border: 1px solid rgba(249, 210, 112, 0.16);
  box-shadow: 0 26px 60px rgba(0, 0, 0, 0.5), inset 0 0 0 1px rgba(255, 255, 255, 0.03);
  overflow: hidden;
}

.hero-copy {
  display: grid;
  gap: 0.65rem;
  align-content: start;
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
  font-size: clamp(2rem, 2.4vw + 1rem, 2.8rem);
  line-height: 1.1;
}

h2 {
  margin: 0;
  font-size: clamp(1.6rem, 1.5vw + 1rem, 2.1rem);
  line-height: 1.2;
}

.lede {
  margin: 0;
  color: #dbe8ff;
  max-width: 780px;
}

.hero-chips {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 0.2rem;
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.5rem 0.85rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(249, 210, 112, 0.18);
  color: #f7f1e7;
  font-weight: 700;
  font-size: 0.95rem;
}

.hero-panel {
  position: relative;
  border-radius: 20px;
  padding: 1.25rem;
  background: linear-gradient(135deg, rgba(249, 210, 112, 0.12), rgba(0, 0, 0, 0.3)), rgba(6, 6, 8, 0.9);
  border: 1px solid rgba(249, 210, 112, 0.3);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(255, 255, 255, 0.03);
  display: grid;
  gap: 0.9rem;
  overflow: hidden;
}

.panel-halo {
  position: absolute;
  inset: 10% 12% auto;
  height: 60%;
  background: radial-gradient(circle at 10% 14%, rgba(249, 210, 112, 0.18), transparent 42%),
    radial-gradient(circle at 90% 30%, rgba(118, 225, 255, 0.12), transparent 40%);
  filter: blur(10px);
  opacity: 0.8;
  pointer-events: none;
}

.panel-head,
.panel-list,
.panel-foot {
  position: relative;
  z-index: 1;
}

.panel-eyebrow {
  margin: 0;
  color: #f9d270;
  font-size: 0.82rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  font-weight: 700;
}

.panel-title {
  margin: 0.2rem 0;
  font-size: 1.3rem;
  font-weight: 800;
}

.panel-subtitle {
  margin: 0;
  color: #d6e4ff;
}

.panel-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  gap: 0.7rem;
}

.panel-list li {
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.7rem;
  align-items: start;
  padding: 0.7rem 0.8rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
}

.icon {
  font-size: 1.1rem;
}

.label {
  margin: 0;
  color: #f9d270;
  font-weight: 700;
}

.value {
  margin: 0;
  color: #e8f0ff;
}

.panel-foot {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 0.7rem;
  padding: 0.75rem 0.85rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.35);
  border: 1px solid rgba(249, 210, 112, 0.2);
}

.panel-cta {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.65rem 0.95rem;
  border-radius: 10px;
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  text-decoration: none;
  font-weight: 800;
  box-shadow: 0 12px 30px rgba(249, 210, 112, 0.32);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.panel-cta:hover,
.panel-cta:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 16px 40px rgba(201, 144, 56, 0.36);
}

.micro {
  margin: 0;
  color: #c7d7f7;
  font-size: 0.95rem;
}

.impressum-details {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

.card {
  background: rgba(8, 8, 10, 0.86);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 22px;
  padding: 1.4rem;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(249, 210, 112, 0.05);
  display: grid;
  gap: 0.9rem;
}

.card-head {
  display: grid;
  gap: 0.3rem;
}

.detail-list {
  margin: 0;
  padding: 0;
  display: grid;
  gap: 0.6rem;
}

.detail-row {
  display: grid;
  grid-template-columns: minmax(140px, 0.8fr) minmax(0, 1fr);
  gap: 0.5rem 1rem;
  padding: 0.75rem 0.85rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
}

dt {
  margin: 0;
  color: #f9d270;
  font-weight: 700;
}

dd {
  margin: 0;
  color: #e8f0ff;
}

.oversight {
  position: relative;
}

.oversight-card {
  position: relative;
  padding: 1.5rem;
  border-radius: 24px;
  background: rgba(7, 9, 16, 0.9);
  border: 1px solid rgba(249, 210, 112, 0.14);
  box-shadow: 0 22px 60px rgba(0, 0, 0, 0.52), inset 0 0 0 1px rgba(255, 255, 255, 0.02);
  overflow: hidden;
  display: grid;
  gap: 1rem;
}

.oversight-glow {
  position: absolute;
  inset: 12% -10% auto;
  height: 60%;
  background: linear-gradient(110deg, rgba(249, 210, 112, 0.22), transparent 50%),
    radial-gradient(circle at 82% 36%, rgba(118, 225, 255, 0.12), transparent 38%);
  filter: blur(30px);
  opacity: 0.8;
  pointer-events: none;
}

.oversight-head,
.oversight-grid {
  position: relative;
  z-index: 1;
}

.oversight-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 0.85rem;
}

.oversight-tile {
  padding: 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  display: grid;
  gap: 0.35rem;
  min-height: 140px;
}

.tile-label {
  margin: 0;
  color: #f9d270;
  font-weight: 800;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  font-size: 0.9rem;
}

.tile-value {
  margin: 0;
  color: #dbe8ff;
  line-height: 1.5;
  display: grid;
  gap: 0.2rem;
}

.tile-link {
  color: #f9d270;
  font-weight: 700;
  word-break: break-all;
  text-decoration: none;
}

.tile-link:hover,
.tile-link:focus-visible {
  text-decoration: underline;
}

.tile-note {
  color: #c7d7f7;
}

.liability {
  display: grid;
  gap: 1rem;
}

.liability-head {
  display: grid;
  gap: 0.4rem;
}

.liability-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 0.9rem;
}

.liability-card {
  padding: 1rem;
  border-radius: 16px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.05);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.35);
  display: grid;
  gap: 0.35rem;
}

.liability-title {
  margin: 0;
  color: #f9d270;
  font-weight: 800;
}

.liability-text {
  margin: 0;
  color: #e2eaff;
}

.liability-bottom {
  padding: 0.9rem 1rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(249, 210, 112, 0.2);
}

@media (max-width: 720px) {
  .impressum-hero,
  .oversight-card {
    padding: 1.1rem;
  }

  .detail-row {
    grid-template-columns: 1fr;
  }
}
</style>
