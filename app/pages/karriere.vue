<script setup lang="ts">
  import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

  type Benefit = {
    icon: string
    title: string
    description: string
  }

  type Track = {
    title: string
    description: string
    accent: 'gold' | 'cyan'
    link: string
  }

  type Position = {
    title: string
    category: string
    description: string
    link: string
  }

  const benefits: Benefit[] = [
    {
      icon: '📈',
      title: 'Stabiler Wirtschaftszweig',
      description: 'Einsätze in einem resilienten Markt mit langfristigen Partnerschaften und klaren Abläufen.'
    },
    {
      icon: '🤝',
      title: 'Teamkultur mit Haltung',
      description:
        'Ehrliche Kommunikation, kurze Wege und Führungskräfte, die selbst aus der Praxis kommen.'
    },
    {
      icon: '🛠️',
      title: 'Moderne Ausstattung',
      description: 'PSA, digitale Einsatzsteuerung und Dokumentation, damit du sicher und effizient arbeitest.'
    },
    {
      icon: '🎯',
      title: 'Individuelle Entwicklung',
      description: 'Weiterbildungen, Zusatzberechtigungen und Unterstützung bei neuen Qualifikationen.'
    },
    {
      icon: '💡',
      title: 'Abwechslungsreiche Projekte',
      description: 'Cargo, Bau, Terminal und Hafen – wir kombinieren Routine mit spannenden Spezialaufgaben.'
    },
    {
      icon: '🌿',
      title: 'Gesund bleiben',
      description: 'Gesundheitsangebote, planbare Schichten und feste Ansprechpartner für deine Einsatzplanung.'
    }
  ]

  const tracks: Track[] = [
    {
      title: 'Ausbildung & Praktikum',
      description:
        'Starte nach der Schule in einem vielseitigen Berufsbild. Wir begleiten dich mit Mentoring, sicherer Technik und klaren Lernpfaden.',
      accent: 'gold',
      link: '#jobs'
    },
    {
      title: 'Fach- & Führungskraft',
      description:
        'Bringe deine Erfahrung ein oder wage den nächsten Schritt. Wir bieten dir Verantwortung, Struktur und modern ausgestattete Einsätze.',
      accent: 'cyan',
      link: '#jobs'
    }
  ]

  const positions: Position[] = [
    {
      title: 'Triebfahrzeugführer (m/w/d) – Cargo & Bau',
      category: 'Lok & Traktion',
      description: 'Fahre moderne Loks im Güter- und Bauzugverkehr – sicher, pünktlich und dokumentiert.',
      link: '/kontakt'
    },
    {
      title: 'Zweiwegebaggerführer (m/w/d)',
      category: 'Bau & Infrastruktur',
      description: 'Bewege Schotter, Schwellen und Schienen punktgenau und unterstützt Baustellenlogistik.',
      link: '/kontakt'
    },
    {
      title: 'Rangierbegleiter:in Bau (m/w/d)',
      category: 'Rangier & Sicherheit',
      description: 'Sorge auf Baustellen und Werksgleisen für sichere Rangierabläufe und reibungslose Übergaben.',
      link: '/kontakt'
    },
    {
      title: 'Wagenprüfer:in (m/w/d) – bis Stufe 4',
      category: 'Prüfung & Qualität',
      description:
        'Führe Wagenprüfungen durch, erstelle Lauffähigkeitsuntersuchungen und dokumentiere auditierbar.',
      link: '/kontakt'
    }
  ]

  const scrollY = ref(0)
  const heroDrift = computed(() => Math.min(scrollY.value * 0.08, 60))
  const gradientShift = computed(() => Math.min(scrollY.value * 0.04, 30))

  const handleScroll = () => {
    scrollY.value = window.scrollY
  }

  onMounted(() => {
    scrollY.value = window.scrollY
    window.addEventListener('scroll', handleScroll, { passive: true })
  })

  onBeforeUnmount(() => {
    window.removeEventListener('scroll', handleScroll)
  })
</script>

<template>
  <div class="career-page">
    <section class="career-hero">
      <div class="career-hero__bg" aria-hidden="true">
        <div class="career-hero__beam career-hero__beam--one" :style="{ transform: `translateY(${heroDrift}px)` }" />
        <div class="career-hero__beam career-hero__beam--two" :style="{ transform: `translateY(${heroDrift * -1}px)` }" />
        <div
          class="career-hero__glow career-hero__glow--left"
          :style="{ transform: `translateY(${gradientShift}px)` }"
        />
        <div
          class="career-hero__glow career-hero__glow--right"
          :style="{ transform: `translateY(${gradientShift * -1}px)` }"
        />
      </div>
      <div class="career-hero__grid">
        <div class="career-hero__copy">
          <p class="eyebrow">Karriere bei Babylon Bahndienste</p>
          <h1>Dein nächster Schritt auf der Schiene beginnt hier.</h1>
          <p class="career-hero__lead">
            Wir verbinden Sicherheit, moderne Technik und eine Kultur des Miteinanders. Ganz gleich, ob du einsteigst,
            quer einsteigst oder den nächsten Karriereschritt planst – wir machen den Weg frei.
          </p>
          <div class="career-hero__actions">
            <a class="cta cta--solid" href="#jobs">
              Zu den Stellenangeboten
              <span aria-hidden="true">↗</span>
            </a>
            <a class="cta cta--ghost" href="#bewerbung">Initiativ bewerben</a>
          </div>
          <div class="career-hero__meta">
            <div class="meta-card">
              <p class="meta-label">Onboarding</p>
              <p class="meta-value">innerhalb von 2 Wochen</p>
            </div>
            <div class="meta-card">
              <p class="meta-label">Betriebliche Altersvorsorge</p>
              <p class="meta-value">inklusive Zuschuss</p>
            </div>
            <div class="meta-card">
              <p class="meta-label">Weiterbildung</p>
              <p class="meta-value">individuelle Budgets</p>
            </div>
            <div class="meta-card">
              <p class="meta-label">Arbeitsumfeld</p>
              <p class="meta-value">Familiär und kollegial</p>
            </div>
          </div>
        </div>

        <div class="career-hero__visual">
          <div class="career-hero__card">
            <div class="career-hero__card-header">
              <p class="eyebrow">Miteinander arbeiten</p>
              <p class="headline">Wir setzen auf Teams, die Verantwortung übernehmen und Sicherheit leben.</p>
            </div>
            <div class="career-hero__stats">
              <div class="stat">
                <span class="stat__value">30</span>
                <span class="stat__label">Urlaubstage</span>
              </div>
              <div class="stat">
                <span class="stat__value">24/7</span>
                <span class="stat__label">Disposition</span>
              </div>
              <div class="stat">
                <span class="stat__value">100%</span>
                <span class="stat__label">PSA gestellt</span>
              </div>
            </div>
            <div class="career-hero__image">
              <img src="/images/cta-bild.jpg" alt="Team von Babylon Bahndienste im Einsatz" loading="lazy">
              <div class="career-hero__badge">
                <span class="dot dot--gold" aria-hidden="true" />
                Teil eines starken Teams
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section class="section">
      <div class="section__header">
        <div>
          <p class="eyebrow">Deine Vorteile</p>
          <h2>Was dich bei uns erwartet</h2>
          <p class="section__lead">
            Wir bieten dir planbare Einsätze, moderne Ausstattung und ein Umfeld, das Weiterentwicklung aktiv fördert.
          </p>
        </div>
      </div>
      <div class="benefits-grid">
        <article v-for="benefit in benefits" :key="benefit.title" class="benefit-card">
          <div class="benefit-card__icon" aria-hidden="true">{{ benefit.icon }}</div>
          <div>
            <h3>{{ benefit.title }}</h3>
            <p>{{ benefit.description }}</p>
          </div>
        </article>
      </div>
    </section>

    <section class="section">
      <div class="section__header section__header--split">
        <div>
          <p class="eyebrow">Einstieg</p>
          <h2>Wähle deinen Weg</h2>
          <p class="section__lead">
            Ob Ausbildung, Quereinstieg oder Führung: Wir begleiten dich mit klaren Onboarding-Pfaden und Mentor:innen.
          </p>
        </div>
        <NuxtLink to="/kontakt" class="cta cta--gold">Kontakt aufnehmen</NuxtLink>
      </div>
      <div class="tracks-grid">
        <article v-for="track in tracks" :key="track.title" class="track-card" :data-accent="track.accent">
          <div class="track-card__badge" :data-accent="track.accent" aria-hidden="true" />
          <h3>{{ track.title }}</h3>
          <p>{{ track.description }}</p>
          <a :href="track.link" class="text-link">
            Zu den Stellenangeboten
            <span aria-hidden="true">↗</span>
          </a>
        </article>
      </div>
    </section>

    <section class="section section--panel">
      <div class="culture-panel">
        <div class="culture-panel__content">
          <p class="eyebrow">Team & Kultur</p>
          <h2>Wir arbeiten partnerschaftlich, sicherheitsführend und mit klarer Kommunikation.</h2>
          <p class="section__lead">
            Bei uns stehen Menschen im Mittelpunkt. Wir setzen auf Respekt, Verlässlichkeit und echte Teamarbeit – auf
            der Schiene, auf der Baustelle und im Austausch miteinander.
          </p>
          <ul class="culture-list">
            <li>Feste Ansprechpartner:innen in der Disposition</li>
            <li>Transparente Schicht- und Einsatzplanung</li>
            <li>Dokumentierte Unterweisungen und moderne Tools</li>
          </ul>
        </div>
        <div class="culture-panel__contact">
          <div class="contact-card">
            <div class="contact-card__header">
              <p class="eyebrow">Ansprechpartner</p>
              <h3>Sanharip Aras</h3>
              <p class="contact-card__role">Leitung</p>
            </div>
            <div class="contact-card__details">
              <a class="contact-link" href="mailto:karriere@babylon-bahndienste.de">
                <span aria-hidden="true">✉️</span>
                info@babylon-bahndienste.de
              </a>
              <a class="contact-link" href="tel:+491607050005">
                <span aria-hidden="true">📞</span>
                +49 123 456 789
              </a>
            </div>
            <NuxtLink to="/kontakt" class="cta cta--solid contact-card__cta">
              Gespräch vereinbaren
              <span aria-hidden="true">↗</span>
            </NuxtLink>
          </div>
        </div>
      </div>
    </section>

    <section id="jobs" class="section">
      <div class="section__header section__header--split">
        <div>
          <p class="eyebrow">Offene Stellen</p>
          <h2>Werde Teil unseres Teams</h2>
          <p class="section__lead">
            Aktuell suchen wir Kolleg:innen, die Einsatzbereitschaft, Sicherheitsbewusstsein und Freude am Miteinander
            mitbringen.
          </p>
        </div>
        <a class="cta cta--ghost" href="#bewerbung">Initiativbewerbung</a>
      </div>
      <div class="positions-list">
        <article v-for="position in positions" :key="position.title" class="position-card">
          <div class="position-card__meta">
            <p class="position-card__category">{{ position.category }}</p>
            <span class="pill">{{ position.location }}</span>
            <span class="pill pill--ghost">{{ position.shift }}</span>
          </div>
          <h3>{{ position.title }}</h3>
          <p>{{ position.description }}</p>
          <div class="position-card__actions">
            <NuxtLink :to="position.link" class="cta cta--inline">
              Gespräch anfragen
              <span aria-hidden="true">↗</span>
            </NuxtLink>
          </div>
        </article>
      </div>
    </section>

    <section id="bewerbung" class="section section--panel">
      <div class="application">
        <div class="application__header">
          <div>
            <p class="eyebrow">Initiativbewerbung</p>
            <h2>Nichts Passendes dabei? Überzeuge uns trotzdem.</h2>
            <p class="section__lead">
              Wir freuen uns über jede Bewerbung von Menschen, die Eisenbahn leben. Erzähle uns von deinen Stärken,
              Qualifikationen und Einsatzwünschen.
            </p>
          </div>
          <span class="application__accent">Jetzt bewerben!</span>
        </div>
        <form class="application__form" @submit.prevent>
          <div class="form-grid">
            <label class="field">
              <span>Vorname</span>
              <input type="text" name="vorname" placeholder="Max">
            </label>
            <label class="field">
              <span>Nachname *</span>
              <input type="text" name="nachname" placeholder="Mustermann" required>
            </label>
            <label class="field">
              <span>Firma</span>
              <input type="text" name="firma" placeholder="Optional">
            </label>
            <label class="field">
              <span>E-Mail *</span>
              <input type="email" name="email" placeholder="beispiel@mail.de" required>
            </label>
            <label class="field">
              <span>Telefonnummer *</span>
              <input type="tel" name="telefon" placeholder="+49" required>
            </label>
            <label class="field">
              <span>Wunsch-Einsatzort</span>
              <input type="text" name="standort" placeholder="z. B. Hannover, Hamburg">
            </label>
          </div>
          <label class="field field--wide">
            <span>Nachricht</span>
            <textarea
              name="nachricht"
              rows="5"
              placeholder="Erzähle uns von deinen Qualifikationen und Einsatzwünschen."
            ></textarea>
          </label>
          <div class="upload-row">
            <label class="upload">
              <input type="file" name="anhang" accept="application/pdf">
              <span>PDF-Datei anhängen (optional)</span>
            </label>
            <button class="cta cta--solid" type="submit">
              Absenden
              <span aria-hidden="true">→</span>
            </button>
          </div>
        </form>
      </div>
    </section>
  </div>
</template>

<style scoped>
.career-page {
  display: flex;
  flex-direction: column;
  gap: 4rem;
  padding: 1.5rem 1.25rem 4rem;
  color: #e9f2ff;
}

.section {
  max-width: 1100px;
  width: 100%;
  margin: 0 auto;
}

.section--panel {
  width: 100%;
}

.section__header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.section__header--split {
  align-items: center;
}

.section__lead {
  max-width: 640px;
  color: #c7d4ec;
  margin: 0.4rem 0 0;
}

.eyebrow {
  text-transform: uppercase;
  letter-spacing: 0.08em;
  font-size: 0.75rem;
  color: #f9d270;
  margin: 0 0 0.5rem;
}

.career-hero {
  position: relative;
  overflow: hidden;
  border-radius: 24px;
  border: 1px solid rgba(249, 210, 112, 0.12);
  background: radial-gradient(circle at 16% 20%, rgba(249, 210, 112, 0.1), transparent 40%),
    radial-gradient(circle at 78% 10%, rgba(87, 176, 255, 0.12), transparent 42%),
    #0b0b0f;
  box-shadow: 0 35px 80px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(255, 255, 255, 0.03);
}

.career-hero__bg {
  position: absolute;
  inset: 0;
  pointer-events: none;
  overflow: hidden;
}

.career-hero__beam {
  position: absolute;
  width: 120%;
  height: 280px;
  filter: blur(60px);
  opacity: 0.5;
}

.career-hero__beam--one {
  top: -20px;
  left: -10%;
  background: linear-gradient(90deg, rgba(249, 210, 112, 0.2), rgba(255, 122, 195, 0.12));
}

.career-hero__beam--two {
  bottom: -40px;
  right: -12%;
  background: linear-gradient(90deg, rgba(87, 176, 255, 0.18), rgba(255, 122, 195, 0.12));
}

.career-hero__glow {
  position: absolute;
  width: 360px;
  height: 360px;
  filter: blur(90px);
  opacity: 0.4;
}

.career-hero__glow--left {
  top: 18%;
  left: 6%;
  background: radial-gradient(circle, rgba(249, 210, 112, 0.4), transparent 60%);
}

.career-hero__glow--right {
  bottom: 10%;
  right: 8%;
  background: radial-gradient(circle, rgba(87, 176, 255, 0.35), transparent 60%);
}

.career-hero__grid {
  position: relative;
  display: grid;
  grid-template-columns: 1.15fr 1fr;
  gap: 2rem;
  padding: 2.5rem;
}

.career-hero__copy h1 {
  margin: 0 0 0.5rem;
  font-size: clamp(1.9rem, 2.8vw, 2.6rem);
  line-height: 1.1;
}

.career-hero__lead {
  margin: 0.4rem 0 1rem;
  color: #c7d4ec;
}

.career-hero__chips {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin: 1rem 0 0.5rem;
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.45rem 0.75rem;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.05);
  color: #fefefe;
  border: 1px solid rgba(249, 210, 112, 0.22);
  font-weight: 600;
  font-size: 0.9rem;
}

.chip--ghost {
  border-color: rgba(255, 255, 255, 0.12);
  color: #c7d4ec;
}

.chip--accent {
  border-color: rgba(87, 176, 255, 0.45);
  background: rgba(87, 176, 255, 0.12);
}

.career-hero__actions {
  display: flex;
  gap: 0.75rem;
  align-items: center;
  margin-top: 1rem;
  flex-wrap: wrap;
}

.cta {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.75rem 1.1rem;
  border-radius: 12px;
  border: 1px solid rgba(249, 210, 112, 0.35);
  color: #0c0a05;
  text-decoration: none;
  font-weight: 700;
  letter-spacing: 0.01em;
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease, color 0.2s ease;
}

.cta--solid {
  background: linear-gradient(135deg, #f9d270, #c99038);
  box-shadow: 0 15px 35px rgba(249, 210, 112, 0.28);
}

.cta--ghost {
  background: rgba(255, 255, 255, 0.04);
  color: #fefefe;
  border-color: rgba(255, 255, 255, 0.15);
}

.cta--gold {
  background: linear-gradient(135deg, #f9d270, #c99038);
  color: #0c0a05;
  border-color: rgba(249, 210, 112, 0.65);
  box-shadow: 0 18px 36px rgba(249, 210, 112, 0.35), 0 0 0 1px rgba(249, 210, 112, 0.1);
}

.cta--inline {
  padding: 0.35rem 0;
  background: transparent;
  border: none;
  color: #f9d270;
  box-shadow: none;
}

.cta:hover,
.cta:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 20px 40px rgba(249, 210, 112, 0.35);
}

.cta--ghost:hover,
.cta--ghost:focus-visible {
  color: #ffffff;
  box-shadow: 0 15px 35px rgba(0, 0, 0, 0.35);
}

.cta--gold:hover,
.cta--gold:focus-visible {
  transform: translateY(-3px) scale(1.01);
  box-shadow: 0 24px 48px rgba(249, 210, 112, 0.45), 0 0 0 1px rgba(249, 210, 112, 0.16);
}

.career-hero__meta {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 0.75rem;
  margin-top: 1.5rem;
}

.meta-card {
  padding: 0.85rem 1rem;
  border-radius: 14px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.06);
}

.meta-label {
  margin: 0;
  font-size: 0.85rem;
  color: #c7d4ec;
}

.meta-value {
  margin: 0.2rem 0 0;
  font-weight: 700;
  color: #fff7de;
}

.career-hero__visual {
  display: flex;
  align-items: stretch;
}

.career-hero__card {
  width: 100%;
  display: grid;
  gap: 1rem;
  padding: 1.25rem;
  border-radius: 20px;
  background: rgba(7, 7, 9, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(249, 210, 112, 0.06);
}

.career-hero__card-header {
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(255, 255, 255, 0.06);
  border-radius: 16px;
  padding: 1rem;
}

.headline {
  margin: 0.1rem 0 0;
  color: #fff7de;
  font-weight: 700;
}

.career-hero__stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 0.75rem;
}

.stat {
  padding: 0.9rem 1rem;
  border-radius: 14px;
  background: linear-gradient(135deg, rgba(249, 210, 112, 0.12), rgba(87, 176, 255, 0.08));
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.stat__value {
  display: block;
  font-size: 1.4rem;
  font-weight: 800;
}

.stat__label {
  color: #c7d4ec;
}

.career-hero__image {
  position: relative;
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.career-hero__image img {
  display: block;
  width: 100%;
  height: 240px;
  object-fit: cover;
}

.career-hero__badge {
  position: absolute;
  bottom: 12px;
  left: 12px;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.35rem 0.65rem;
  border-radius: 12px;
  background: rgba(0, 0, 0, 0.6);
  color: #fefefe;
  font-weight: 700;
  border: 1px solid rgba(255, 255, 255, 0.12);
}

.benefits-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 1rem;
}

.benefit-card {
  padding: 1rem;
  border-radius: 16px;
  background: rgba(7, 7, 9, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.35);
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 0.75rem;
  align-items: start;
}

.benefit-card h3 {
  margin: 0;
  font-size: 1.1rem;
}

.benefit-card p {
  margin: 0.25rem 0 0;
  color: #c7d4ec;
}

.benefit-card__icon {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  display: grid;
  place-items: center;
  background: rgba(249, 210, 112, 0.12);
  font-size: 1.3rem;
}

.tracks-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 1rem;
}

.track-card {
  position: relative;
  padding: 1.2rem;
  border-radius: 18px;
  background: rgba(7, 7, 9, 0.8);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.04);
}

.track-card h3 {
  margin: 0;
}

.track-card p {
  margin: 0.5rem 0 0.75rem;
  color: #c7d4ec;
}

.track-card__badge {
  position: absolute;
  inset: 0;
  border-radius: 18px;
  pointer-events: none;
  opacity: 0.35;
  filter: blur(50px);
}

.track-card__badge[data-accent='gold'] {
  background: radial-gradient(circle at 30% 30%, rgba(249, 210, 112, 0.4), transparent 60%);
}

.track-card__badge[data-accent='cyan'] {
  background: radial-gradient(circle at 30% 30%, rgba(87, 176, 255, 0.35), transparent 60%);
}

.text-link {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  color: #f9d270;
  text-decoration: none;
  font-weight: 700;
}

.section--panel .culture-panel {
  max-width: 1100px;
  margin: 0 auto;
}

.culture-panel {
  display: grid;
  grid-template-columns: 1.2fr 0.8fr;
  gap: 1.5rem;
  padding: 1.5rem;
  border-radius: 20px;
  background: linear-gradient(135deg, rgba(249, 210, 112, 0.07), rgba(87, 176, 255, 0.05));
  border: 1px solid rgba(255, 255, 255, 0.06);
}

.culture-list {
  list-style: none;
  padding: 0;
  margin: 1rem 0 0;
  display: grid;
  gap: 0.5rem;
  color: #c7d4ec;
}

.culture-list li::before {
  content: '•';
  color: #f9d270;
  margin-right: 0.5rem;
}

.culture-panel__contact {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.contact-card {
  width: 100%;
  max-width: 360px;
  padding: 1.2rem;
  border-radius: 18px;
  background: radial-gradient(circle at 30% 30%, rgba(249, 210, 112, 0.12), transparent 55%),
    #0c0c10;
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 18px 50px rgba(0, 0, 0, 0.4);
}

.contact-card__role {
  margin: 0.15rem 0 0;
  color: #c7d4ec;
}

.contact-card__details {
  display: grid;
  gap: 0.4rem;
  margin: 0.75rem 0;
}

.contact-link {
  color: #fefefe;
  text-decoration: none;
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
}

.contact-card__cta {
  width: 100%;
  justify-content: center;
}

.positions-list {
  display: grid;
  gap: 1rem;
}

.position-card {
  padding: 1.1rem;
  border-radius: 16px;
  background: linear-gradient(135deg, #f9d270, #d8a63e);
  border: 1px solid #c99038;
  box-shadow: 0 16px 40px rgba(201, 144, 56, 0.35);
  color: #0c0a05;
}

.position-card__meta {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  align-items: center;
  margin-bottom: 0.4rem;
}

.position-card__category {
  margin: 0;
  font-weight: 700;
  color: #0c0a05;
}

.pill {
  display: inline-flex;
  align-items: center;
  gap: 0.3rem;
  padding: 0.35rem 0.65rem;
  border-radius: 999px;
  background: #fbe4a3;
  color: #0c0a05;
  border: 1px solid #c99038;
  font-weight: 600;
}

.pill--ghost {
  background: #f6cf68;
  border-color: #a8761d;
  color: #0c0a05;
}

.position-card h3 {
  margin: 0;
  color: #0c0a05;
}

.position-card p {
  margin: 0.4rem 0 0.75rem;
  color: #0c0a05;
}

.position-card__actions {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.position-card__actions .cta--inline {
  color: #0c0a05;
  font-weight: 800;
  box-shadow: none;
}

.position-card__actions .cta--inline:hover,
.position-card__actions .cta--inline:focus-visible {
  box-shadow: none;
  text-decoration: underline;
}

.section--panel .application {
  max-width: 1100px;
  margin: 0 auto;
}

.application {
  padding: 1.5rem;
  border-radius: 22px;
  background: linear-gradient(135deg, rgba(0, 0, 0, 0.75), rgba(7, 7, 9, 0.9));
  border: 1px solid rgba(255, 255, 255, 0.08);
  box-shadow: 0 22px 70px rgba(0, 0, 0, 0.5);
}

.application__header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 1rem;
  margin-bottom: 1rem;
}

.application__accent {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.7rem 1rem;
  border-radius: 999px;
  background: #f9d270;
  color: #0c0a05;
  font-weight: 800;
  letter-spacing: 0.02em;
  box-shadow: 0 12px 30px rgba(249, 210, 112, 0.35);
}

.application__form {
  display: grid;
  gap: 1rem;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 320px));
  justify-content: space-between;   /* verteilt Restbreite als Abstand */
  gap: 1.1rem 1.75rem;              /* mehr Abstand zwischen den Spalten */
}

.field {
  display: grid;
  gap: 0.35rem;
  font-weight: 600;
  color: #fefefe;
  min-width: 0;
}

.field span {
  font-size: 0.9rem;
  color: #c7d4ec;
}

.field input,
.field textarea {
  width: 100%;
  padding: 0.85rem 1rem;
  border-radius: 14px;
  border: 1px solid rgba(255, 255, 255, 0.16);
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.06), rgba(255, 255, 255, 0.03));
  backdrop-filter: blur(6px);
  color: #fefefe;
  font-size: 1rem;
  font-family: inherit;
  box-shadow: 0 12px 26px rgba(0, 0, 0, 0.28),
    inset 0 0 0 1px rgba(255, 255, 255, 0.03);  transition: border-color 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
}

.field input:focus,
.field textarea:focus {
  outline: 2px solid rgba(249, 210, 112, 0.65);
  outline-offset: 2px;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.35);
}

.field--wide textarea {
  resize: vertical;
  min-height: 140px;
}

.field--wide {
  grid-column: 1 / -1;
}

.upload-row {
  display: flex;
  flex-wrap: wrap;
  gap: 0.75rem;
  align-items: center;
  justify-content: space-between;
}

.upload {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.7rem 1rem;
  border-radius: 12px;
  border: 1px dashed rgba(255, 255, 255, 0.2);
  background: rgba(255, 255, 255, 0.03);
  cursor: pointer;
  color: #c7d4ec;
}

.upload input {
  display: none;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  display: inline-block;
}

.dot--gold {
  background: #f9d270;
}

.career-hero__visual img {
  border-radius: 12px;
}

.career-hero__card img {
  display: block;
}

.career-hero__card .eyebrow {
  margin-bottom: 0.2rem;
}

.career-hero__card .headline {
  font-size: 1.1rem;
}

.career-hero__card .stat__label {
  font-size: 0.9rem;
}

.career-hero__card .stat__value {
  font-size: 1.5rem;
}

@media (max-width: 960px) {
  .career-hero__grid,
  .culture-panel {
    grid-template-columns: 1fr;
  }

  .career-hero__grid {
    padding: 1.6rem;
  }

  .culture-panel__contact {
    justify-content: flex-start;
  }
}

@media (max-width: 720px) {
  .career-page {
    padding: 1rem 1rem 3rem;
  }

  .career-hero__actions {
    flex-direction: column;
    align-items: stretch;
  }

  .career-hero__meta {
    grid-template-columns: 1fr;
  }

  .upload-row {
    flex-direction: column;
    align-items: stretch;
  }

  .application__header {
    flex-direction: column;
  }
}

@media (max-width: 960px) {
  .form-grid {
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    justify-content: stretch;
    gap: 1.1rem 1.25rem;
  }
}
</style>
