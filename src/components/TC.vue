<template>
  <div class="container">
    <section class="form box">
      <h1 class="title">Dein Großes Geschäft</h1>
        <b-field label="Große Geschäfte pro Tag">
            <b-numberinput min="0" v-model="poopsPerDay" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Abwischer pro Geschäft">
            <b-numberinput min="0" v-model="wipesPerPoop" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Blatt pro Abwisch">
            <b-numberinput min="0" v-model="papesPerWipe" controls-alignment="right"></b-numberinput>
        </b-field>
        <h1 class="title">Dein kleines Geschäft</h1>
        <b-field label="Kleine Geschäfte pro Tag">
            <b-numberinput min="0" v-model="peesPerDay" controls-alignment="right"></b-numberinput>
        </b-field>
        <b-field label="Blatt pro Abwisch">
            <b-numberinput min="0" v-model="papesPerPee" controls-alignment="right"></b-numberinput>
        </b-field>
        <h1 class="title">Über dich</h1>
        <b-field>
          <b-checkbox v-model="menstruationCheckbox"
            true-value="Ja, ich menstruiere."
            false-value="Nein, ich menstruiere nicht.">
            {{ this.menstruationCheckbox }}
          </b-checkbox>
          <b-tooltip
            label="Je nach Menstruationsprodukt steigt der Klopapierverbrauch. Wir haben in einer nicht representativen Umfrage einen Mehrverbrauch im Durchschnitt von 33% im Monat ermittelt"
            position="is-top"
            size="is-large"
            multilined>
            <b-button label="Info" type="is-dark" />
          </b-tooltip>
        </b-field>
        <b-field label="Wie viele Menschen leben in deinem Haushalt?">
            <b-numberinput min="1" v-model="peopleInHouse" controls-alignment="right"></b-numberinput>
        </b-field>
    </section>
    <section class="section is-small box container is-max-desktop yellow">
      <!--h1 class="title">Ergebnis</h1-->
      <div class="center">
          Du brauchst pro Monat
        <h1 class="superstrong">{{ this.rollsResult }} Rollen</h1>
        bzw.
        <h1 class="superstrong">{{ Math.ceil(this.rollsResult / 8) }} Packung(en)</h1>
        Goldeimer Klopapier.
      </div>
      <br>
      <h1 class="title">Zeitraum</h1>
      <b-field class="peeriod">
          <b-slider :min="1" :max="6" v-model="peeriot" aria-label="Zeitraum" :tooltip="false">
              <b-slider-tick :value="1">Jeden Monat</b-slider-tick>
              <b-slider-tick :value="2">Alle 2 Monate</b-slider-tick>
              <b-slider-tick :value="3">Alle 3 Monate</b-slider-tick>
              <b-slider-tick :value="4">Alle 4 Monate</b-slider-tick>
              <b-slider-tick :value="5">Alle 5 Monate</b-slider-tick>
              <b-slider-tick :value="6">Alle 6 Monate</b-slider-tick>
          </b-slider>
      </b-field>
      <div class="center">
      Du solltest dir jeden {{ this.peeriot }}. Monat eine/n <h1 class="superstrong">{{ this.monthResult }}</h1> liefern lassen.
    </div>
    <b-field class="center">
      <!--onclick="window.location.href = 'https://goldeimer.de/klopapier'-->
      <b-button class="g-button"><a href="https://goldeimer.de/klopapier" target="_blank">Jetzt Bestellen!</a></b-button>
    </b-field>
    </section>
    <section class="section is-small box container is-max-desktop">
      <h1 class="title">Umweltschutz</h1>
        <strong>Du tust was gutes</strong> alle Profite laufen in unsere Vision <strong>Alle für Klos, Klos für Alle</strong> und gegenüber herrkömmlichen Klopapier auf Frischholzbasis sparst du mit unserem zertifizierten <strong>Recycling</strong> Klopapier pro Monat ca.*:
      <table class="center">
        <tr>
          <strong>{{ Math.round(((this.rollsPerMonth * this.rollWeight * 3) * this.peopleInHouse) * 100) / 100 }} kWh</strong> Energie
        </tr>
        <tr>
          <strong>{{ Math.round(((this.rollsPerMonth * this.rollWeight * 2.2) * this.peopleInHouse) * 100) / 100 }} kg </strong> Frischholz
        </tr>
        <tr>
          <strong>{{ Math.round(((this.rollsPerMonth * this.rollWeight * 35) * this.peopleInHouse) * 100) / 100 }} Liter</strong> virtuelles Wasser
        </tr>
        <!--tr>
          <strong>{{ Math.round(((this.rollsPerMonth * this.rollWeight * 12) * this.peopleInHouse) * 100) / 100 }} </strong> Chemischer Sauerstoffbedarf (CSB)
        </tr-->
      </table>
      <p>
        Das mag für den einzelnen Haushalt eventuell nach gar nicht so viel klingen, aber wenn mensch bedenkt, dass etwa 50 Millionen Menschen nur in Deutschland täglich Klopapier aus Frischholz verwenden, nehmen die Ergebnisse erstaunliche Dimensionen an.
      </p>
      <p class="mini">
        * FÖP-Daten auf Basis der Ökobilanzen des Umweltbundesamtes (2000) und des IFEU Instituts (2008) sowie des 2. Entwurf des BVT(Beste verfügbare Techniken)-Merkblattes für die Zellstoff und Papierherstellung (D2), 16 2012
      </p>
      <p class="mini">
        ** Es ist unmöglich, einen exakten Wert für Wasser- und Energieverbrauch, Abwasserbelastung und Emissionen über die gesamte Papier- und Zellstoff- industrie hinweg anzugeben. Jede Fabrik und jede Papiersorte hat unter- schiedliche Produktionsstandards. Nachfolgend sind Durchschnittswerte dargestellt, um einen Vergleich zwischen Recycling- und Primärfaserpapier zu ermöglichen.
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
      menstruationCheckbox: 'Ja, ich menstruiere.',
      poopsPerDay: 1,
      peopleInHouse: 1,
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
      return (Math.ceil(this.rollsPerMonth) * this.peopleInHouse)
    },
    blatt () {
      return (((this.poopsPerDay * (this.wipesPerPoop * this.papesPerWipe)) + (this.peesPerDay * this.papesPerPee) + this.menstruation))
    },
    aboResult () {
      let abo
      const aboResult = (this.rollsResult / 8)
      if (aboResult >= 81) {
        abo = 'Palette'
      } else if (aboResult >= 27) {
        abo = 'XXL Supervorrat'
      } else if (aboResult >= 9) {
        abo = 'Jahresvorrat'
      } else {
        abo = 'Family Pack'
      }
      return abo
    },
    monthResult () {
      let abo
      const aboResult = (this.rollsResult / 8 * this.peeriot)
      if (aboResult <= 9) {
        abo = 'Family Pack'
      } else if (aboResult <= 27) {
        abo = 'Jahresvorrat'
      } else if (aboResult <= 81) {
        abo = 'XXL Supervorrat'
      } else {
        abo = 'Palette'
      }
      return abo
    },
    // energieResult () {
    //   return Math.ceil((this.rollsPerMonth / this.rollsPerPackage) / 9)
    // },
    // woodResult () {
    //   return Math.ceil((this.rollsPerMonth / this.rollsPerPackage) / 9)
    // },
    // waterResult () {
    //   return Math.ceil((this.rollsPerMonth / this.rollsPerPackage) / 9)
    // },
    // csbResult () {
    //   return Math.ceil((this.rollsPerMonth / this.rollsPerPackage) / 9)
    // },
    menstruation () {
      let menstruation
      if (this.menstruationCheckbox === 'Ja, ich menstruiere.') {
        menstruation = 33
      } else {
        menstruation = 0
      }
      return menstruation
    }
  }
}
</script>

<style lang="scss">
//@import  "/src/assets/sass/main.scss";

.peeriod {
  padding-bottom: 2em;
}

.center {
  text-align: center;
  margin: 2em auto;
}

a {
  text-decoration: none;
  color: #ffe500 !important;
}
a:visited {
  text-decoration: none;
  color: #ffe500;
}

.mini {
  font-size: 0.75em;
  padding: 5px;
}

.superstrong {
  font-size: 2em;
  font-family: Veneer;
}

.yellow {
  background-color: #ffe500 !important;
}
</style>
