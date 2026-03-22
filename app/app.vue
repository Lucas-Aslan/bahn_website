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

      <button
        class="menu-toggle"
        type="button"
        :aria-expanded="isMobileMenuOpen"
        aria-controls="mobile-navigation"
        aria-label="Menü öffnen oder schließen"
        @click="toggleMobileMenu"
      >
        <span />
        <span />
        <span />
      </button>

      <nav
        id="mobile-navigation"
        class="nav-links"
        :class="{ 'is-open': isMobileMenuOpen }"
        aria-label="Hauptnavigation"
      >
        <NuxtLink to="/" class="nav-link">Startseite</NuxtLink>

      <div class="nav-dropdown" role="presentation">
      </div>

        <NuxtLink to="/leistungen" class="nav-link">Leistungen</NuxtLink>
        
        <NuxtLink to="/karriere" class="nav-link">Karriere</NuxtLink>

        <NuxtLink to="/about" class="nav-link">Über uns</NuxtLink>
      </nav>

      <div class="cta-group">
        <NuxtLink to="/kontakt" class="cta-button">
          Kontakt
        </NuxtLink>
      </div>
    </header>

    <main class="page-body">
      <NuxtPage />
    </main>

    <AnimatedFooter />
  </div>
</template>

<script setup lang="ts">
const isMobileMenuOpen = ref(false)
const route = useRoute()

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

watch(
  () => route.path,
  () => {
    isMobileMenuOpen.value = false
  }
)
</script>

<style scoped>
:global(:root) {
  --color-rose: #0b7a5c;
  --color-rose-soft: #55a58d;
  --color-forest: #2f3439;
  --color-forest-soft: #4a525a;
  --color-cream: #ffffff;
  --color-paper: #ffffff;
  --color-ink: #1f2520;
  --color-muted: #3f564c;
  --color-border: rgba(47, 52, 57, 0.14);
}

:global(html) {
  font-size: 112.5%;
}

:global(body) {
  margin: 0;
  font-family: 'Inter', 'Segoe UI', system-ui, -apple-system, sans-serif;
  background:
    radial-gradient(circle at 16% 18%, rgba(11, 122, 92, 0.12) 0, transparent 26%),
    radial-gradient(circle at 82% 10%, rgba(47, 52, 57, 0.12) 0, transparent 22%),
    linear-gradient(135deg, #ffffff, var(--color-cream));
  color: var(--color-ink);
  min-height: 100vh;
  -webkit-font-smoothing: antialiased;
}

:global(::selection) {
  background: rgba(11, 122, 92, 0.18);
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
  background: linear-gradient(transparent 96%, rgba(47, 52, 57, 0.06)),
    linear-gradient(90deg, transparent 96%, rgba(11, 122, 92, 0.06));
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
  padding: 0.85rem clamp(1rem, 3vw, 2.5rem);
  margin: 0;
  width: 100%;
  border-radius: 0;
  background: var(--color-forest);
  color: #ffffff;
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
  box-shadow: 0 12px 30px rgba(11, 122, 92, 0.28);
}

.brand-kicker {
  margin: 0;
  font-size: 0.7rem;
  color: rgba(255, 255, 255, 0.78);
}

.brand-name {
  margin: 0;
  font-size: 1.05rem;
  font-weight: 700;
}

.menu-toggle {
  display: none;
  width: 44px;
  height: 44px;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.4);
  background: rgba(255, 255, 255, 0.08);
  align-items: center;
  justify-content: center;
  flex-direction: column;
  gap: 0.28rem;
  cursor: pointer;
  margin-left: auto;
}

.menu-toggle span {
  width: 18px;
  height: 2px;
  border-radius: 999px;
  background: #ffffff;
  display: block;
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
  color: #ffffff;
  background: rgba(255, 255, 255, 0.12);
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
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.12), inset 0 0 0 1px rgba(47, 52, 57, 0.08);
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
  border: 1px solid rgba(11, 122, 92, 0.18);
  transition: background 0.2s ease, transform 0.2s ease, border-color 0.2s ease;
}

.dropdown-item:hover,
.dropdown-item:focus-visible {
  background: linear-gradient(135deg, rgba(11, 122, 92, 0.14), rgba(47, 52, 57, 0.14));
  border-color: rgba(47, 52, 57, 0.28);
  transform: translateX(4px);
}

.cta-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.65rem 1.1rem;
  border-radius: 12px;
  background: var(--color-rose);
  color: #ffffff;
  font-weight: 800;
  text-decoration: none;
  letter-spacing: 0.02em;
  box-shadow: 0 18px 45px rgba(11, 122, 92, 0.35);
  transition: transform 0.18s ease, box-shadow 0.18s ease;
}

.cta-button:hover,
.cta-button:focus-visible {
  transform: translateY(-1px) scale(1.01);
  box-shadow: 0 22px 55px rgba(11, 122, 92, 0.42);
}

.cta-group {
  display: inline-flex;
  align-items: center;
  gap: 0.65rem;
  margin-right: clamp(1rem, 4vw, 4rem);
}

.page-body {
  padding: 0 clamp(0.9rem, 3vw, 1.5rem) 3rem;
  max-width: 1200px;
  margin: 0 auto;
  width: 100%;
  box-sizing: border-box;
}

@media (min-width: 1200px) {
  :global(html) {
    font-size: 120%;
  }
}

@media (max-width: 900px) {
  :global(html) {
    font-size: 106.25%;
  }

  .topbar {
    grid-template-columns: auto auto;
    row-gap: 0;
    text-align: left;
    column-gap: 0.8rem;
  }

  .menu-toggle {
    display: inline-flex;
    margin-left: 0;
    justify-self: start;
  }

  .nav-links {
    grid-column: 1 / -1;
    display: none;
    width: 100%;
    flex-direction: column;
    align-items: stretch;
    gap: 0.45rem;
    padding-top: 0.35rem;
  }

  .nav-links.is-open {
    display: flex;
  }

  .cta-group {
    grid-column: 1 / -1;
    width: 100%;
    display: none;
    margin-right: 0;
  }

  .nav-links.is-open ~ .cta-group {
    display: inline-flex;
    flex-direction: column;
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

@media (max-width: 700px) {
  :global(html) {
    font-size: 100%;
  }
}

@media (max-width: 560px) {
  .topbar {
    padding-inline: 0.8rem;
  }

  .brand {
    justify-content: flex-start;
    text-align: left;
  }

  .nav-link,
  .cta-button {
    width: 12.5rem;
    box-sizing: border-box;
  }
}
</style>
