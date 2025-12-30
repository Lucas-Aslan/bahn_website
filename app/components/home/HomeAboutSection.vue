<template>
  <section id="about" class="about section js-reveal">
    <div class="about__entry-overlay" aria-hidden="true">
      <span class="about__beam about__beam--left" />
      <span class="about__beam about__beam--center" />
      <span class="about__beam about__beam--right" />
    </div>
    <div class="about__inner">
      <div class="about__header">
        <div class="about__eyebrow">
          <p class="eyebrow">Über uns</p>
          <span class="about__spark" aria-hidden="true" />
        </div>
        <h2>Präzision, Sicherheit, partnerschaftlich.</h2>
        <p class="section__lead">
          Babylon Bahndienste ist Ihr zuverlässiger Partner rund um die Schiene: erfahrene Teams, klare Abläufe und
          konsequente Sicherheit – von der Planung bis zum Einsatz vor Ort. Transparente Kommunikation und saubere
          Dokumentation halten Projekte planbar und den Bahnbetrieb stabil.
        </p>

        <div class="about__highlights" role="list">
          <div class="about__highlight" role="listitem">
            <span class="about__pulse" aria-hidden="true" />
            <div>
              <p class="about__label">Einsatzsicherheit</p>
              <p class="about__description">Sicherungslogik, Unterweisungen und Reporting bleiben lückenlos.</p>
            </div>
          </div>
          <div class="about__highlight" role="listitem">
            <span class="about__pulse about__pulse--gold" aria-hidden="true" />
            <div>
              <p class="about__label">Planung bis Umsetzung</p>
              <p class="about__description">Von der Crew-Dispo bis zum Vor-Ort-Einsatz alles aus einer Hand.</p>
            </div>
          </div>
          <div class="about__highlight" role="listitem">
            <span class="about__pulse about__pulse--cyan" aria-hidden="true" />
            <div>
              <p class="about__label">Partnerschaftlich</p>
              <p class="about__description">Transparente Kommunikation und proaktive Abstimmung mit Auftraggebern.</p>
            </div>
          </div>
        </div>

        <div class="about__actions">
          <NuxtLink to="/about" class="about__cta about__cta--solid">
            Mehr über uns
            <span aria-hidden="true">→</span>
          </NuxtLink>
        </div>
      </div>
    </div>
  </section>
</template>
