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

<style scoped>
:global(body) {
  margin: 0;
  font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
  background:
    radial-gradient(circle at 12% 18%, rgba(0, 0, 0, 0.6) 0, #050505 46%),
    radial-gradient(circle at 86% 12%, rgba(249, 210, 112, 0.09) 0, transparent 22%),
    #040404;
  color: #e8f0ff;
  min-height: 100vh;
}

.app-shell {
  position: relative;
  min-height: 100vh;
  overflow: hidden;
}

.tech-grid {
  position: absolute;
  inset: 0;
  background: linear-gradient(transparent 96%, rgba(249, 210, 112, 0.07)),
    linear-gradient(90deg, transparent 96%, rgba(249, 210, 112, 0.07));
  background-size: 32px 32px;
  mask-image: radial-gradient(circle at 50% 50%, rgba(0, 0, 0, 0.6), transparent 65%);
  pointer-events: none;
}

.topbar {
  position: sticky;
  top: 0;
  z-index: 10;
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 1.25rem;
  padding: 0.8rem 1.3rem;
  margin: 1rem auto;
  max-width: 1100px;
  width: calc(100% - 2rem);
  border-radius: 18px;
  background: rgba(10, 10, 12, 0.88);
  backdrop-filter: blur(14px);
  box-shadow: 0 20px 60px rgba(0, 0, 0, 0.45), inset 0 0 0 1px rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(249, 210, 112, 0.18);
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.brand-icon {
  width: 38px;
  height: 38px;
  display: grid;
  place-items: center;
  border-radius: 12px;
  background: linear-gradient(135deg, #f9d270, #c99038);
  color: #0c0a05;
  font-weight: 800;
  box-shadow: 0 10px 30px rgba(249, 210, 112, 0.35);
}

.brand-kicker {
  margin: 0;
  font-size: 0.7rem;
  color: #f6e6b4;
}

.brand-name {
  margin: 0;
  font-size: 1.05rem;
  font-weight: 700;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 0.35rem;
  justify-content: center;
}

.nav-link {
  position: relative;
  padding: 0.55rem 0.9rem;
  border-radius: 10px;
  color: #e8f0ff;
  text-decoration: none;
  font-weight: 600;
  letter-spacing: 0.01em;
  transition: color 0.2s ease, background 0.2s ease, transform 0.2s ease;
  background: transparent;
  border: none;
  cursor: pointer;
}

.nav-link::after {
  content: '';
  position: absolute;
  left: 12px;
  right: 12px;
  bottom: 10px;
  height: 2px;
  border-radius: 999px;
  background: linear-gradient(90deg, transparent, #f9d270, #c99038, transparent);
  opacity: 0;
  transform: translateY(6px);
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.nav-link:hover,
.nav-link:focus-visible {
  color: #ffffff;
  background: rgba(249, 210, 112, 0.08);
  transform: translateY(-1px);
}

.nav-link:hover::after,
.nav-link:focus-visible::after {
  opacity: 1;
  transform: translateY(0);
}

.nav-dropdown {
  position: relative;
}

.dropdown-panel {
  position: absolute;
  left: 0;
  top: calc(100% + 10px);
  min-width: 240px;
  padding: 0.5rem;
  border-radius: 14px;
  background: rgba(6, 6, 8, 0.96);
  box-shadow: 0 25px 70px rgba(0, 0, 0, 0.5), inset 0 0 0 1px rgba(249, 210, 112, 0.1);
  opacity: 0;
  pointer-events: none;
  transform: translateY(-6px);
  transition: opacity 0.2s ease, transform 0.2s ease;
  display: grid;
  gap: 0.35rem;
}

.nav-dropdown:hover .dropdown-panel,
.nav-dropdown:focus-within .dropdown-panel {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}

.dropdown-item {
  text-decoration: none;
  color: #e8f0ff;
  padding: 0.7rem 0.85rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.02);
  border: 1px solid rgba(249, 210, 112, 0.12);
  transition: background 0.2s ease, transform 0.2s ease, border-color 0.2s ease;
}

.dropdown-item:hover,
.dropdown-item:focus-visible {
  background: linear-gradient(135deg, rgba(249, 210, 112, 0.18), rgba(201, 144, 56, 0.22));
  border-color: rgba(249, 210, 112, 0.35);
  transform: translateX(4px);
}

.cta-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.65rem 1.1rem;
  border-radius: 12px;
  background: linear-gradient(120deg, #f9d270, #c99038);
  color: #0c0a05;
  font-weight: 800;
  text-decoration: none;
  letter-spacing: 0.02em;
  box-shadow: 0 18px 45px rgba(249, 210, 112, 0.32);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.cta-button:hover,
.cta-button:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 55px rgba(201, 144, 56, 0.4);
}

.page-body {
  padding: 1rem 1.5rem 3rem;
  max-width: 1200px;
  margin: 0 auto;
}

@media (max-width: 900px) {
  .topbar {
    grid-template-columns: 1fr;
    row-gap: 0.8rem;
    text-align: center;
  }

  .nav-links {
    flex-wrap: wrap;
  }

  .cta-button {
    width: 100%;
  }

  .nav-dropdown {
    width: 100%;
  }

  .dropdown-panel {
    position: relative;
    opacity: 1;
    pointer-events: auto;
    transform: none;
    top: 0;
    margin-top: 0.35rem;
  }
}
</style>
