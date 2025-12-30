<template>
  <div class="app-shell">
    <div class="tech-grid" aria-hidden="true" />
    <header class="topbar">
      <NuxtRouteAnnouncer />
      <div class="brand">
        <div class="brand-icon">LOG</div>
        <div>
          <p class="brand-kicker">Babylon Bahndienste</p>
          <!-- <p class="brand-name">Babylon Bahndienste UG</p> -->
        </div>
      </div>

      <nav class="nav-links" aria-label="Hauptnavigation">
        <NuxtLink to="/" class="nav-link">Startseite</NuxtLink>

      <div class="nav-dropdown" role="presentation">
        <button class="nav-link" type="button">Leistungen</button>
      </div>

        <NuxtLink to="/karriere" class="nav-link">Karriere</NuxtLink>

        <NuxtLink to="/about" class="nav-link">Über uns</NuxtLink>
      </nav>

      <NuxtLink to="/kontakt" class="cta-button">
        Kontakt
      </NuxtLink>
    </header>

    <main class="page-body">
      <NuxtPage />
    </main>

    <AnimatedFooter />
  </div>
</template>
