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
