<template>
  <div class="row q-dialog container" style="padding: 20px; max-width: 800px">
    <h4>
      Bestellung - Plätze für die Gottesdienste am Heiligen Abend 2021 – St.
      Bonifaz
    </h4>
    <p class="text-subtitle1">
      Corona-bedingt werden wir für die Vergabe der Sitzplätze am Heiligen Abend
      wieder das Vergabesystem vom letzten Jahr einsetzen.
      <!--Bitte haben Sie
      Verständnis dafür, dass wir bei der <b>Anmeldung</b> auch abfragen, unter
      welchen <b>Corona-Regeln</b> Sie an einem zugangsbeschränkten Gottesdienst
      teilnehmen können oder vielleicht sogar wollen. Diese Angabe ist natürlich
      freiwillig, gibt uns aber die Möglichkeit, unser Gottesdienstangebot an
      die dann vorgeschriebenen Bedingungen (vermutlich mindestens Maske und
      Abstand) anzupassen.-->
    </p>
    <ul class="text-subtitle1">
      <li>2 Kinderchristmetten (15:30, 16:30 Uhr) und</li>
      <li>2 Christmetten (18:00, 22:30 Uhr)</li>
    </ul>
    <p class="text-subtitle1">
      Aufgrund der aktuellen Lage können wir alle Gottesdienste ohne 2G oder 3G
      Beschränkungen durchführen. Es bleiben jedoch Abstand, Maskenpflicht und
      reservierte Plätze.
    </p>
    <p class="text-subtitle1">
      <b>
        Bitte füllen Sie das untenstehende Formular aus und senden es bis 19.12.
        an die angegebene E-Mail Adresse. Sie erleichtern uns damit die Arbeit.
      </b>
    </p>

    <p class="text-subtitle1">
      Drücken Sie dafür auf das Feld
      <span style="background-color: #1976d2; color: white; padding: 5px">
        "E-MAIL ÖFFNEN"</span
      >
      am Ende des Formulars<br />
      Sie erhalten dann per E-Mail bis zum 22.12.2021 eine Rückmeldung, für
      welchen Gottesdienst und auf welchen Platz wir Sie eingeteilt haben.
      <br />
      <b>Bitte bringen Sie diese Platz - Information mit zum Gottesdienst.</b>
    </p>

    <p class="text-subtitle1">
      Bitte benutzen Sie dieses Formular auch, um bereits abgegebene
      <b>Bestellungen zu stornieren oder zu ändern</b>. Senden Sie die E-Mail
      bitte <b>unverändert</b> ab. Zusätzliche Hinweise können Sie im Feld
      „Bemerkungen“ angeben.
    </p>
    <form style="min-width: 300px; max-width: 600px">
      <q-input
        ref="nachname"
        bottom-slots
        filled
        label="Name"
        v-model="formData.nachname"
        :rules="[(val) => !!val || 'Bitte geben Sie Ihren Nachnamen an']"
      >
        <template v-slot:hint></template>
      </q-input>

      <q-input
        ref="vorname"
        bottom-slots
        filled
        label="Vorname"
        v-model="formData.vorname"
        :rules="[(val) => !!val || 'Bitte geben Sie Ihren Vornamen an']"
        required
      >
        <template v-slot:hint></template>
      </q-input>
      <q-input
        style="max-width: 600px"
        bottom-slots
        filled
        label="Telefonnummer für Rückfragen"
        name="telefon"
        v-model="formData.telefon"
      >
      </q-input>

      <q-select
        ref="plaetze"
        style="max-width: 600px"
        bottom-slots
        label="Anzahl Plätze"
        name="anzahl"
        filled
        v-model="formData.anzahl"
        :options="[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]"
      >
        <template v-slot:hint>
          Anzahl 0 bedeutet eine Stornierung aller Plätze
        </template>
      </q-select>
      <br />

      <q-select
        ref="wunsch1"
        label="Terminwunsch"
        bottom-slots
        filled
        v-model="formData.wunschtermin"
        :options="[
          'Kinderchristmette: 15:30 Uhr',
          'Kinderchristmette: 16:30 Uhr',
          'Christmette: 18:00 Uhr',
          'Christmette: 22:30 Uhr',
        ]"
        :rules="[(val) => !!val || 'Sie müssen einen Terminwunsch angeben']"
      >
      </q-select>

      <q-select
        ref="wunsch2"
        label="Alternativwunsch"
        bottom-slots
        filled
        v-model="formData.alternativtermin"
        :options="[
          'Kinderchristmette: 15:30 Uhr',
          'Kinderchristmette: 16:30 Uhr',
          'Christmette: 18:00 Uhr',
          'Christmette: 22:30 Uhr',
        ]"
        :rules="[
          (val) => !!val || 'Sie müssen auch einen Ersatz Terminwunsch angeben',
        ]"
      >
      </q-select>

      <br />

      <q-input
        style="max-width: 600px"
        autogrow
        bottom-slots
        filled
        label="Bemerkung"
        name="bemerkung"
        :rules="[(val) => val.length <= 200 || 'Max. 200 Zeichen']"
        v-model="formData.bemerkung"
      >
      </q-input>
      <br />
      <q-btn
        color="primary"
        icon="mail"
        icon-right="send"
        @click="setEmailLink()"
        label="EMail öffnen"
      >
        <!--         :href="maillink" -->
      </q-btn>

      <!--q-btn
        ref="btnreally"
        color="secondary"
        icon="mail"
        label="EMail öffnen"
        :href="maillink"
      >

      </q-btn-->
      <p>
        <br />Mit der Abgabe dieser Bestellung erkläre ich mich damit
        einverstanden, dass die angegebenen persönliche Daten von der Pfarrei
        St. Bonifaz auf Grundlage von Art. 6, Abs.1a DS-GVO verarbeitet und für
        die Dauer der Organisation der Gottesdienste am Heiligen Abend 2021
        gespeichert oder in Papierform ablegt werden.
      </p>
    </form>
    <hr />

    <!--   -->
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { openURL } from "quasar";

export default defineComponent({
  name: "pageIndex",
  props: ["para"],
  components: {},
  data() {
    return {
      email: "reservierung@st-bonifaz-regensburg.de",
      formData: {
        nachname: "", //'Sonnleiter',
        vorname: "", //'Hans-Juergen',
        telefon: "",
        adresse: "",
        anzahl: "", //'10',
        wunschtermin: "", //'Kinderchristmette: 16:00 Uhr',
        alternativtermin: "", //'Kinderchristmette: 14:00 Uhr',
        bemerkung: "",
      },
      mailtext: "",
      formError: {
        email: { status: true, text: "keine gültige E-Mail!" },
      },
      maillink: "",
    };
  },
  watch: {
    // wenn sich was ändert an den Parametern,
    // hole die Daten neu!
    para(val) {
      // this.GetPages()
    },
  },
  methods: {
    /**
     * Asyncroner Aufruf der verfügbaren Elemente im Cockpitstore
     * Die Parameter werden dazu aus einem Spezialabsatz gelesen.
     *
     */
    async validateForm() {
      this.$refs.nachname.validate();
      this.$refs.vorname.validate();
      this.$refs.plaetze.validate();
      this.$refs.wunsch1.validate();
      this.$refs.wunsch2.validate();

      if (
        this.$refs.nachname.hasError ||
        this.$refs.vorname.hasError ||
        this.$refs.plaetze.hasError ||
        this.$refs.wunsch1.hasError ||
        this.$refs.wunsch2.hasError
      ) {
        return false;
      }
      return true;
    },

    /**
     * Da
     */
    async setEmailLink() {
      let result = await this.validateForm();
      if (!result) {
        return;
      }
      let datenschutz = `
Einwilligungserklärung zur Datenspeicherung:

Mit der Abgabe dieser Bestellung erkläre ich mich damit einverstanden, dass die angegebenen persönliche Daten von der Pfarrei St. Bonifaz auf Grundlage von Art. 6, Abs.1a DS-GVO verarbeitet und für die Dauer der Organisation der Gottesdienste am Heiligen Abend 2021 gespeichert oder in Papierform ablegt werden.`;

      let einfuerungstext = `Sehr geehrte Damen und Herren,

hiermit schicke ich ihnen meinen Reservierungswunsch für die Weihnachtsgottesdienste am 24.12. der etwaige vorherige Reservierungswünsche ersetzt. 

(die Anzahl 0 bei den gewünschten Plätzen bedeutet eine komplette Stornierung).

`;
      let body = einfuerungstext + "\n\n";
      body =
        body +
        "Name:\t" +
        this.formData.nachname +
        " " +
        this.formData.vorname +
      "\n";
      body = body + "Telefonnr:\t" + this.formData.telefon + "\n";      
      body = body + "Gewünschte Plätze:\t" + this.formData.anzahl + "\n";
      body = body + "Terminwunsch:\t" + this.formData.wunschtermin + "\n";
      body =
        body + "Alternativtermin:\t" + this.formData.alternativtermin + "\n";
      body = body + "Bemerkung:\n" + this.formData.bemerkung + "\n";
      body = body + datenschutz;

      this.maillink =
        "mailto:" +
        this.email +
        "?subject=Reservierungswunsch für die Gottesdienste am 24.12.2021 – St. Bonifaz&body=" +
        encodeURIComponent(body);
      openURL(this.maillink);
    },
  },
  created() {},
});
</script>
