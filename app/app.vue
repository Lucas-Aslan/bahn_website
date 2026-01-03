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
:global(:root) {
  --color-rose: #c7758b;
  --color-rose-soft: #dba1b2;
  --color-forest: #004831;
  --color-forest-soft: #1b6c50;
  --color-cream: #f6f1eb;
  --color-paper: #fffaf3;
  --color-ink: #1f2520;
  --color-muted: #3f564c;
  --color-border: rgba(0, 72, 49, 0.14);
}

:global(body) {
  margin: 0;
  font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
  background:
    radial-gradient(circle at 16% 18%, rgba(199, 117, 139, 0.12) 0, transparent 26%),
    radial-gradient(circle at 82% 10%, rgba(0, 72, 49, 0.12) 0, transparent 22%),
    linear-gradient(135deg, #fffdf8, var(--color-cream));
  color: var(--color-ink);
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
}

:global(::selection) {
  background: rgba(199, 117, 139, 0.18);
  color: var(--color-ink);
}

.app-shell {
  position: relative;
  min-height: 100vh;
  overflow: hidden;
}

.tech-grid {
  position: absolute;
  inset: 0;
  background: linear-gradient(transparent 96%, rgba(0, 72, 49, 0.06)),
    linear-gradient(90deg, transparent 96%, rgba(199, 117, 139, 0.06));
  background-size: 32px 32px;
  mask-image: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.5), transparent 65%);
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
  padding: 0.85rem 1.3rem;
  margin: 1rem auto;
  max-width: 1100px;
  width: calc(100% - 2rem);
  border-radius: 18px;
  background: #000000;
  color: #f5f5f5;
  box-shadow: 0 16px 50px rgba(0, 0, 0, 0.4), inset 0 0 0 1px rgba(255, 255, 255, 0.08);
  border: 1px solid rgba(255, 255, 255, 0.12);
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
  background: linear-gradient(135deg, var(--color-rose), var(--color-forest));
  color: #ffffff;
  font-weight: 800;
  box-shadow: 0 12px 30px rgba(199, 117, 139, 0.28);
}

.brand-kicker {
  margin: 0;
  font-size: 0.7rem;
  color: var(--color-muted);
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
  color: #ffffff;
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
  background: linear-gradient(90deg, transparent, var(--color-rose), var(--color-forest), transparent);
  opacity: 0;
  transform: translateY(6px);
  transition: opacity 0.2s ease, transform 0.2s ease;
}

.nav-link:hover,
.nav-link:focus-visible {
  color: var(--color-forest);
  background: rgba(0, 72, 49, 0.06);
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
  background: rgba(255, 250, 243, 0.96);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.12), inset 0 0 0 1px rgba(0, 72, 49, 0.08);
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
  color: var(--color-ink);
  padding: 0.7rem 0.85rem;
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(199, 117, 139, 0.18);
  transition: background 0.2s ease, transform 0.2s ease, border-color 0.2s ease;
}

.dropdown-item:hover,
.dropdown-item:focus-visible {
  background: linear-gradient(135deg, rgba(199, 117, 139, 0.14), rgba(0, 72, 49, 0.14));
  border-color: rgba(0, 72, 49, 0.28);
  transform: translateX(4px);
}

.cta-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.65rem 1.1rem;
  border-radius: 12px;
  background: var(--color-forest);
  color: #ffffff;
  font-weight: 800;
  text-decoration: none;
  letter-spacing: 0.02em;
  box-shadow: 0 18px 45px rgba(0, 72, 49, 0.25);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.cta-button:hover,
.cta-button:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 55px rgba(0, 72, 49, 0.32);
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
