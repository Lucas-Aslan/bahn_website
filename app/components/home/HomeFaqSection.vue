<script setup lang="ts">
import { ref } from 'vue'

type FAQItem = {
  question: string
  answer: string
}

const faqItems: FAQItem[] = [
  {
    question: 'Wie schnell können Sie Fachpersonal für meinen Einsatz stellen?',
    answer:
      'Unsere Disposition ist 24/7 erreichbar. Mit vorhandenen Crew-Pools und Streckenkunde können wir in der Regel binnen 24 Stunden Einsatzpersonal einplanen und nach dokumentierter Sicherheitsunterweisung starten lassen.'
  },
  {
    question: 'Welche Qualifikationen bringen Ihre Triebfahrzeugführer und Rangierbegleiter mit?',
    answer:
      'Unsere Teams verfügen über aktuelle Tauglichkeiten, Zusatzbescheinigungen für Bau- und Güterverkehre sowie Baureihenberechtigungen u. a. für Vossloh DE 12/18, G1206, Siemens BR 248 und Alstom BR 214/203. Rangierbegleiter sind bremsproberechtigt und wagenprüfgeschult.'
  },
  {
    question: 'Übernehmen Sie auch die Einsatzsteuerung und das Reporting?',
    answer:
      'Ja. Wir bieten eine vollständige Einsatzsteuerung inklusive Slot-Management, Statusmeldungen, Tagesreportings und KPI-Tracking. Auftraggeber erhalten feste Ansprechpartner und revisionssichere Dokumentation aus der Leitstelle.'
  },
  {
    question: 'Arbeiten Sie nach EBA-Standards und unterstützen Sie Audits?',
    answer:
      'Wir orientieren uns strikt an EBA-Vorgaben, dokumentieren Unterweisungen, Risikobeurteilungen und Fahrzeugprüfungen digital und unterstützen Sie bei Auditvorbereitung sowie Compliance-Checks.'
  },
  {
    question: 'Decken Sie Projekte deutschlandweit ab?',
    answer:
      'Ja. Wir begleiten Projekte bundesweit – von Güterverkehrskorridoren über Baustellenlogistik bis zu Terminal- und Hafenumschlag. Reise- und Schichtplanung erfolgen zentral, damit Ihre Umläufe stabil bleiben.'
  }
]

const openFaqIndex = ref<number | null>(0)

const toggleFaq = (index: number) => {
  openFaqIndex.value = openFaqIndex.value === index ? null : index
}
</script>

<template>
  <section class="faq section js-reveal" id="faq">
    <div class="section__header faq__header">
      <div>
        <p class="eyebrow">FAQ</p>
        <h2>Häufige Fragen zu Babylon Bahndiensten</h2>
        <p class="section__lead">
          Klarheit zu Verfügbarkeit, Qualifikationen und Abläufen – damit Ihr Einsatz planbar bleibt.
        </p>
      </div>
      <NuxtLink to="/kontakt" class="faq__cta">
        Individuelle Anfrage stellen
        <span aria-hidden="true">↗</span>
      </NuxtLink>
    </div>

    <div class="faq__list" role="list">
      <article
        v-for="(item, index) in faqItems"
        :key="item.question"
        class="faq__item"
        role="listitem"
      >
        <button
          class="faq__trigger"
          type="button"
          :aria-expanded="openFaqIndex === index"
          :id="`faq-question-${index}`"
          :aria-controls="`faq-panel-${index}`"
          @click="toggleFaq(index)"
        >
          <div class="faq__question">
            <span class="faq__pill">Bahndienste</span>
            <h3>{{ item.question }}</h3>
          </div>
          <span class="faq__icon" aria-hidden="true">
            <span class="faq__icon-line" />
            <span class="faq__icon-line faq__icon-line--vertical" />
          </span>
        </button>
        <Transition name="faq-answer">
          <div
            v-if="openFaqIndex === index"
            :id="`faq-panel-${index}`"
            class="faq__answer"
            role="region"
            :aria-labelledby="`faq-question-${index}`"
          >
            <p>{{ item.answer }}</p>
            <div class="faq__glow" aria-hidden="true" />
          </div>
        </Transition>
      </article>
    </div>
  </section>
</template>

<style scoped>
.faq {
  position: relative;
  overflow: hidden;
  background:
    radial-gradient(circle at 18% 18%, rgba(199, 117, 139, 0.12), transparent 42%),
    radial-gradient(circle at 82% 82%, rgba(0, 72, 49, 0.14), transparent 46%),
    linear-gradient(135deg, var(--color-paper), var(--color-cream));
  border: 1px solid rgba(0, 72, 49, 0.12);
  color: var(--color-ink);
  box-shadow: 0 26px 70px rgba(0, 0, 0, 0.08);
}

.faq__header {
  align-items: center;
}

.faq__cta {
  justify-self: end;
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  padding: 0.85rem 1.15rem;
  border-radius: 12px;
  background: var(--color-forest);
  color: #ffffff;
  text-decoration: none;
  font-weight: 800;
  letter-spacing: 0.02em;
  border: 1px solid rgba(0, 72, 49, 0.24);
  box-shadow: 0 18px 45px rgba(0, 72, 49, 0.2), inset 0 1px 0 rgba(255, 255, 255, 0.6);
  transition: transform 0.2s ease, box-shadow 0.2s ease, background 0.2s ease;
}

.faq__cta:hover,
.faq__cta:focus-visible {
  transform: translateY(-1px);
  box-shadow: 0 22px 55px rgba(0, 0, 0, 0.12);
  color: #ffffff;
}

.faq__list {
  display: grid;
  gap: 0.8rem;
  margin-top: 1rem;
}

.faq__item {
  position: relative;
  overflow: hidden;
  border-radius: 18px;
  border: 1px solid rgba(0, 72, 49, 0.14);
  background: rgba(255, 255, 255, 0.85);
  box-shadow:
    0 16px 40px rgba(0, 0, 0, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.8);
}

.faq__trigger {
  width: 100%;
  border: none;
  background: none;
  color: inherit;
  text-align: left;
  padding: 1.2rem 1.2rem 1.1rem;
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 0.8rem;
  align-items: center;
  cursor: pointer;
}

.faq__item:hover,
.faq__item:focus-within {
  border-color: rgba(199, 117, 139, 0.3);
  box-shadow:
    0 22px 55px rgba(0, 0, 0, 0.12),
    0 0 0 1px rgba(199, 117, 139, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.9);
}

.faq__question {
  display: grid;
  gap: 0.35rem;
}

.faq__question h3 {
  margin: 0;
  font-size: 1.18rem;
  letter-spacing: -0.01em;
  color: var(--color-ink);
}

.faq__pill {
  display: inline-flex;
  width: fit-content;
  align-items: center;
  gap: 0.4rem;
  padding: 0.35rem 0.65rem;
  border-radius: 999px;
  background: rgba(0, 72, 49, 0.08);
  color: var(--color-forest);
  letter-spacing: 0.04em;
  text-transform: uppercase;
  font-weight: 800;
  font-size: 0.78rem;
  border: 1px solid rgba(0, 72, 49, 0.18);
}

.faq__icon {
  position: relative;
  width: 40px;
  height: 40px;
  border-radius: 12px;
  background: rgba(199, 117, 139, 0.1);
  border: 1px solid rgba(199, 117, 139, 0.24);
  display: grid;
  place-items: center;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.8);
  transition: transform 0.2s ease, border-color 0.2s ease;
}

.faq__icon-line {
  position: absolute;
  width: 14px;
  height: 2px;
  border-radius: 999px;
  background: var(--color-forest);
  transition: transform 0.2s ease;
}

.faq__icon-line--vertical {
  transform: rotate(90deg);
}

.faq__trigger[aria-expanded='true'] .faq__icon {
  transform: rotate(180deg);
  border-color: rgba(0, 72, 49, 0.5);
}

.faq__trigger[aria-expanded='true'] .faq__icon-line--vertical {
  transform: rotate(90deg) scaleY(0);
}

.faq__answer {
  position: relative;
  padding: 0 1.2rem 1.2rem;
  color: var(--color-muted);
  line-height: 1.6;
}

.faq__answer p {
  margin: 0;
}

.faq__glow {
  position: absolute;
  inset: -20% -40% 10% auto;
  background: radial-gradient(circle, rgba(199, 117, 139, 0.14), transparent 55%);
  filter: blur(28px);
  opacity: 0.9;
  pointer-events: none;
}

.faq-answer-enter-active,
.faq-answer-leave-active {
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.faq-answer-enter-from,
.faq-answer-leave-to {
  opacity: 0;
  transform: translateY(-6px);
}

@media (max-width: 700px) {
  .faq__header {
    grid-template-columns: 1fr;
    gap: 0.6rem;
  }

  .faq__cta {
    width: 100%;
    justify-content: center;
    text-align: center;
  }

  .faq__trigger {
    grid-template-columns: 1fr;
    align-items: start;
  }

  .faq__icon {
    justify-self: start;
  }
}
</style>
