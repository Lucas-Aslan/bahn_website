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
