<template>
  <section id="about" class="about section js-reveal">
    <p class="eyebrow">Über uns</p>
    <h2>Präzision, Sicherheit, partnerschaftlich.</h2>
    <p class="section__lead">
      Babylon Bahndienste ist Ihr zuverlässiger Partner rund um die Schiene: erfahrene Teams, klare Abläufe und
      konsequente Sicherheit – von der Planung bis zum Einsatz vor Ort. Transparente Kommunikation und saubere
      Dokumentation halten Projekte planbar und den Bahnbetrieb stabil.
    </p>

    <ul class="about__list">
      <li>
        <strong>Einsatzsicherheit:</strong>
        Sicherungslogik, Unterweisungen und Reporting bleiben lückenlos.
      </li>
      <li>
        <strong>Planung bis Umsetzung:</strong>
        Von der Crew-Dispo bis zum Vor-Ort-Einsatz alles aus einer Hand.
      </li>
      <li>
        <strong>Partnerschaftlich:</strong>
        Transparente Kommunikation und proaktive Abstimmung mit Auftraggebern.
      </li>
    </ul>

    <div class="about__facts">
      <p><strong>24/7:</strong> Einsatzbereitschaft</p>
      <p><strong>100%:</strong> Nachvollziehbare Dokumentation</p>
    </div>

    <ol class="about__timeline">
      <li>
        <strong>Briefing & Planung</strong>
        <span>Risiken bewerten, Team abstimmen, Ablauf sichern.</span>
      </li>
      <li>
        <strong>Sicherer Einsatz</strong>
        <span>Vor-Ort-Koordination mit klaren Verantwortlichkeiten.</span>
      </li>
      <li>
        <strong>Reporting & Übergabe</strong>
        <span>Vollständige Dokumentation für Transparenz und Nachweis.</span>
      </li>
    </ol>

    <NuxtLink to="/about" class="about__cta">Mehr über uns →</NuxtLink>
  </section>
</template>

<style scoped>
.about {
  display: grid;
  gap: 1rem;
  background: #ffffff;
}

.about h2 {
  margin: 0;
}

.about .section__lead {
  margin: 0;
}

.about__list,
.about__timeline {
  margin: 0;
  padding: 0;
  display: grid;
  gap: 0.7rem;
}

.about__list {
  list-style: none;
}

.about__list li,
.about__timeline li {
  border: 1px solid rgba(0, 72, 49, 0.14);
  border-radius: 12px;
  padding: 0.8rem 1rem;
  background: rgba(0, 72, 49, 0.03);
}

.about__timeline {
  counter-reset: steps;
  list-style: none;
}

.about__timeline li {
  display: grid;
  gap: 0.2rem;
}

.about__timeline li::before {
  counter-increment: steps;
  content: '0' counter(steps);
  font-weight: 700;
  color: var(--color-forest);
  font-size: 0.85rem;
}

.about__timeline span {
  color: var(--color-muted);
}

.about__facts {
  display: grid;
  gap: 0.6rem;
}

.about__facts p {
  margin: 0;
}

.about__cta {
  justify-self: start;
  display: inline-flex;
  text-decoration: none;
  font-weight: 700;
  color: #ffffff;
  background: var(--color-forest);
  border-radius: 12px;
  padding: 0.7rem 1rem;
}
</style>
