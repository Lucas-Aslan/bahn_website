<template>
  <footer class="footer">
    <div class="footer__glow" aria-hidden="true" />

    <div class="footer__grid">
      <div class="footer__brand">
        <div class="footer__brand-head">


          <div class="footer__brand-text">
            <p class="footer__eyebrow">Bahnlogistik</p>
            <p class="footer__title">Babylon Bahndienste</p>
          </div>
        </div>


        <div class="footer__card footer__contact-card">
          <span class="footer__badge">24/7 Leitstelle</span>
          <p class="footer__card-label">Kontakt</p>
          <p class="footer__card-text">
            Babylon Bahndienste UG (haftungsbeschränkt)<br>
            Frankfurter Weg 27<br>
            33106 Paderborn
          </p>
          <div class="footer__contact-links">
            <span>Telefon: <a href="tel:+49123456789">+49 123 456 789</a></span>
            <span>E-Mail: <a href="mailto:info@babylon-bahndienste.de">info@babylon-bahndienste.de</a></span>
          </div>
          <div class="footer__contact-actions" aria-label="Direkte Kontaktoptionen">
            <a class="footer__action" href="tel:+49123456789">
              <span class="footer__action-dot" aria-hidden="true" />
              Jetzt anrufen
            </a>
            <a class="footer__action" href="mailto:info@babylon-bahndienste.de">
              <span class="footer__action-dot" aria-hidden="true" />
              E-Mail senden
            </a>
          </div>
          <NuxtLink to="/kontakt" class="footer__cta">Kontakt aufnehmen</NuxtLink>
        </div>
      </div>

      <div class="footer__columns">
        <div class="footer__column">
          <p class="footer__heading">Unternehmen</p>
          <ul class="footer__list">
            <li><NuxtLink to="/about">Über uns</NuxtLink></li>
            <li><NuxtLink to="/karriere">Karriere</NuxtLink></li>
            <li><NuxtLink to="/kontakt">Kontakt</NuxtLink></li>
          </ul>
        </div>

        <div class="footer__column">
          <p class="footer__heading">Rechtliches</p>
          <ul class="footer__list">
            <li><NuxtLink to="/impressum">Impressum</NuxtLink></li>
            <li><NuxtLink to="/datenschutz">Datenschutz</NuxtLink></li>
            <li><NuxtLink to="/barrierefreiheit">Barrierefreiheit</NuxtLink></li>
          </ul>
        </div>

        <div class="footer__social">
          <p class="footer__heading">Folgen Sie uns</p>
          <div class="footer__social-list" aria-label="Social Media">
            <a
              class="footer__social-link"
              href="https://www.instagram.com"
              target="_blank"
              rel="noopener"
              aria-label="Instagram"
            >
              <svg class="footer__social-icon" viewBox="0 0 24 24" role="img" aria-hidden="true">
                <path
                  d="M7.5 3h9A4.5 4.5 0 0 1 21 7.5v9A4.5 4.5 0 0 1 16.5 21h-9A4.5 4.5 0 0 1 3 16.5v-9A4.5 4.5 0 0 1 7.5 3Zm0 1.5A3 3 0 0 0 4.5 7.5v9A3 3 0 0 0 7.5 19.5h9A3 3 0 0 0 19.5 16.5v-9A3 3 0 0 0 16.5 4.5h-9Zm9.75 1.05a.9.9 0 1 1-.9.9.9.9 0 0 1 .9-.9ZM12 8.25A3.75 3.75 0 1 1 8.25 12 3.75 3.75 0 0 1 12 8.25Zm0 1.5A2.25 2.25 0 1 0 14.25 12 2.25 2.25 0 0 0 12 9.75Z"
                />
              </svg>
            </a>
            <a
              class="footer__social-link"
              href="https://www.linkedin.com"
              target="_blank"
              rel="noopener"
              aria-label="LinkedIn"
            >
              <svg class="footer__social-icon" viewBox="0 0 24 24" role="img" aria-hidden="true">
                <path
                  d="M6.7 9.25V18H4V9.25h2.7ZM5.36 6a1.57 1.57 0 0 1 1.6 1.54A1.57 1.57 0 0 1 5.36 9 1.57 1.57 0 0 1 3.75 7.54 1.57 1.57 0 0 1 5.36 6Zm4.26 3.25h2.59v1.19h.04a2.84 2.84 0 0 1 2.55-1.4c2.73 0 3.24 1.8 3.24 4.15V18h-2.7v-3.87c0-.92 0-2.11-1.29-2.11s-1.49 1-1.49 2.05V18h-2.7Z"
                />
              </svg>
            </a>
            <a
              class="footer__social-link"
              href="https://www.tiktok.com"
              target="_blank"
              rel="noopener"
              aria-label="TikTok"
            >
              <svg class="footer__social-icon" viewBox="0 0 24 24" role="img" aria-hidden="true">
                <path
                  d="M15.86 6.21a4.6 4.6 0 0 0 .06.62 3.67 3.67 0 0 0 1.52 2.3 3.92 3.92 0 0 0 2.42.76V12a6.58 6.58 0 0 1-2.9-.58 6.83 6.83 0 0 1-.56-.31v4.72a3.57 3.57 0 0 1-.63 2.09 3.76 3.76 0 0 1-3.18 1.7 3.84 3.84 0 0 1-2.12-.6 3.76 3.76 0 0 1-1.32-1.57 3.64 3.64 0 0 1 .81-4.1 3.91 3.91 0 0 1 2.63-1 3.88 3.88 0 0 1 1.06.15v2.16a1.75 1.75 0 0 0-.9-.24 1.74 1.74 0 0 0-.95.29 1.62 1.62 0 0 0-.6.77 1.56 1.56 0 0 0 .13 1.26 1.66 1.66 0 0 0 .74.68 1.73 1.73 0 0 0 .89.13 1.66 1.66 0 0 0 .87-.35 1.83 1.83 0 0 0 .4-.47 1.64 1.64 0 0 0 .18-.6 2.1 2.1 0 0 0 0-.34v-9h2.54a3.44 3.44 0 0 1-.38-1.4Z"
                />
              </svg>
            </a>
          </div>
        </div>
      </div>
    </div>

    <div class="footer__meta">
      <div class="footer__ticker">
        <span class="footer__pulse" aria-hidden="true" />
        <p class="footer__legal">© 2026 Babylon Bahndienste – Präzision auf Schienen.</p>
      </div>
    </div>
  </footer>
</template>
