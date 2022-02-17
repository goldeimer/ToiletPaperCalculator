<template>
  <div class="container">
    <section class="form">
      <h1 class="title">Dein Großes Geschäft</h1>
        <b-field label="große Geschäfte am Tag">
            <b-numberinput min="0" v-model="poopsPerDay" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Abwischer pro Geschäft">
            <b-numberinput min="0" v-model="wipesPerPoop" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Blatt pro Abwisch">
            <b-numberinput min="0" v-model="papesPerWipe" controls-alignment="right"></b-numberinput>
        </b-field>
        <h1 class="title">Dein kleines Geschäft</h1>
        <b-field label="kleine Geschäfte am Tag">
            <b-numberinput min="0" v-model="peesPerDay" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Blatt pro Abwisch">
            <b-numberinput min="0" v-model="papesPerPee" controls-alignment="right"></b-numberinput>
        </b-field>
        <h1 class="title">Über dich</h1>
        <b-field>
          <b-checkbox v-model="menstruationCheckbox"
            true-value="Ja, ich menstruiere"
            false-value="Nein, ich menstruiere nicht">
            {{ this.menstruationCheckbox }}
          </b-checkbox>
          <b-tooltip
            label="Je nach Menstruationsprodukt steigt der Klopapierverbrauch. Wir haben in einer nicht representativen Umfrage einen Mehrverbrauch im Durchschnitt von 33% im Monat ermittelt"
            position="is-top"
            size="is-large"
            multilined>
            <b-button label="info" type="is-dark" />
          </b-tooltip>
        </b-field>
        <b-field label="Wie viele Menschen leben in deinem Haushalt?">
            <b-numberinput min="1" v-model="peeps" controls-alignment="right"></b-numberinput>
        </b-field>
    </section>
    <section class="section is-medium">
      <h1 class="title">Ergebnis</h1>
      <h2>Du brauchst pro Monat {{ this.rollsResult }} Rollen Goldeimer Klopapier</h2>
      <h1 class="title">Peeriod / Zeitraum</h1>
      <b-field label="für welchen Zeitraum möchtest du deine Abogröße berechnen?">
          <b-slider :min="1" :max="6" v-model="peeriot" aria-label="Zeitraum" :tooltip="false">
              <b-slider-tick :value="1">pro Monat</b-slider-tick>
              <b-slider-tick :value="2">alle 2 monate</b-slider-tick>
              <b-slider-tick :value="3">pro viertel Jahr</b-slider-tick>
              <b-slider-tick :value="4">pro Quartal</b-slider-tick>
              <b-slider-tick :value="5">alle 5 monate</b-slider-tick>
              <b-slider-tick :value="6">pro Halbjahr</b-slider-tick>

          </b-slider>
      </b-field>
    </section>
    <section class="section is-small">
      <p>
        Du solltest dir jeden {{ this.peeriot }}. Monat {{ aboResult }} Family-Pack liefern lassen.
      </p>
      <b-button onclick="window.location.href = 'https://goldeimer.de/klopapier'">zum Shop</b-button>
    </section>
    <section class="section is-small">
        Gegenüber herrkömmlichen Klopapier auf Frischholzbasis sparst du pro Monat ca.:
      {{ this.rollsPerMonth * this.rollWeight * 3 }} kWh Energie<br>
      {{ this.rollsPerMonth * this.rollWeight * 2.2 }} kg Frischholz<br>
      {{ this.rollsPerMonth * this.rollWeight * 35 }} liter virtuelles Wasser<br>
      {{ this.rollsPerMonth * this.rollWeight * 12 }} Chemischer Sauerstoffbedarf (CSB)
      <p>
        Das mag für den einzelnen Haushalt eventuell nach gar nicht so viel klingen, aber wenn mensch bedenkt, dass etwa 50 Millionen Menschen nur in Deutschland täglich Klopapier aus Frischholz verwenden, nehmen die Ergebnisse erstaunliche Dimensionen an.
      </p>
      <p>
        Es ist unmöglich, einen exakten Wert für Wasser- und Energieverbrauch, Abwasserbelastung und Emissionen über die gesamte Papier- und Zellstoff- industrie hinweg anzugeben. Jede Fabrik und jede Papiersorte hat unter- schiedliche Produktionsstandards. Nachfolgend sind Durchschnittswerte dargestellt, um einen Vergleich zwischen Recycling- und Primärfaserpapier zu ermöglichen.
        <b-tooltip
          label="FÖP-Daten auf Basis der Ökobilanzen des Umweltbundesamtes (2000) und des IFEU Instituts (2008) sowie des 2. Entwurf des BVT(Beste verfügbare Techniken)-Merkblattes für die Zellstoff und Papierherstellung (D2), 16 2012"
          position="is-top"
          size="is-large"
          multilined>
          <b-button label="info" type="is-dark" />
        </b-tooltip>
      </p>
    </section>
  </div>
</template>

<script>
export default {
  name: 'TC',
  props: {
    // menstruationCheckbox: { type: Boolean, default: true },
    // poopsPerDay: { type: Number, default: 1 },
    // wipesPerPoop: { type: Number, default: 1 },
    // papesPerWipe: { type: Number, default: 1 },
    // peesPerDay: { type: Number, default: 1 },
    // papesPerPee: { type: Number, default: 1 },
    // peeriot: { type: Number, default: 1 },
    // rolls: { type: Number, default: 1 }
  },
  data () {
    return {
      menstruationCheckbox: 'Ja, ich menstruiere',
      poopsPerDay: 1,
      wipesPerPoop: 1,
      papesPerWipe: 1,
      peesPerDay: 1,
      papesPerPee: 1,
      peeriot: 1,
      peeps: 1,
      rollWeight: 0.0901, // Faktor zum Kilo 11,0988
      rollsPerPackage: 8,
      piecesPerRoll: 150,
      daysPerMonth: 30
    }
  },
  computed: {
    rolls () {
      return ((((this.poopsPerDay * (this.wipesPerPoop * this.papesPerWipe)) + (this.peesPerDay * this.papesPerPee) + this.menstruation)) / this.piecesPerRoll)
    },
    rollsPerMonth () {
      return (((((this.poopsPerDay * (this.wipesPerPoop * this.papesPerWipe)) + (this.peesPerDay * this.papesPerPee) + this.menstruation)) / this.piecesPerRoll) * this.daysPerMonth)
    },
    rollsResult () {
      return (Math.ceil(this.rollsPerMonth))
    },
    blatt () {
      return (((this.poopsPerDay * (this.wipesPerPoop * this.papesPerWipe)) + (this.peesPerDay * this.papesPerPee) + this.menstruation))
    },
    aboResult () {
      return Math.ceil((this.rollsPerMonth / this.rollsPerPackage) / 9)
    },
    menstruation () {
      let menstruation
      if (this.menstruationCheckbox === 'Ja, ich menstruiere') {
        menstruation = 33
      } else {
        menstruation = 0
      }
      return menstruation
    }
  }
}
</script>

<style scoped>
</style>
