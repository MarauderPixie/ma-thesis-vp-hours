<template>
  <Experiment title="Institut für Kognitionswissenschaften - Universität Osnabrück" :wide=true>

    <Screen v-bind="$attrs" title="Registrierung für Probandenstunden">
      <Slide>
        <p>Um eine Probandenstunde zu erhalten, benötigen wir deinen Namen, deine Email-Adresse und deine Matrikelnummer.</p>
        <p>Diese Infos werden unabhängig von den Experimentaldaten gespeichert und sind nicht auf diese zurückzuführen.</p>
        <hr />
        <p>
          <label>
            Studiengang: 
            <DropdownInput
              :options="['', 'Cognitive Science (Uni Osnabrück)', 'Psychologie (Uni Osnabrück)', 'Psychologie (Uni Bremen)', 'andere']"
              :response.sync="$magpie.measurements.uni" 
            />
            </label>
        </p>
        <p>
          <label>
            Matrikelnummer:
            <input
              v-model="$magpie.measurements.matrikel"
              type="text"
              placeholder="3.14159265"
            />
          </label>
        </p>
        <p>
          <label>
            Vor- und Nachname:
            <input
              v-model="$magpie.measurements.name"
              type="text"
              placeholder="Quentin Quaderkopf"
            />
          </label>
        </p>
        <p>
          <label>
            Email-Adresse:
            <input
              v-model="$magpie.measurements.email"
              type="text"
              placeholder="uni@osnabrem.de"
            />
          </label>
        </p>
        <p>
          <button @click="$magpie.saveAndNextScreen()">Absenden</button>
        </p>
      </Slide>
    </Screen>

    <Screen v-if="!$magpie.debug">
      <Slide>
        <p>Einen Augenblick, Daten werden übermittelt.</p>
        <Wait :time="0" @done="submit(() => $magpie.nextSlide())" />
      </Slide>
      <Slide>
        <div class="fin">
          <p>Deine Daten wurden übermittelt und du kannst dir voraussichtlich Ende September deine VPh eintragen lassen. Solltest du sie vorher benötigen, melde dich gerne einfach bei <a href="tanton@uos.de">tanton@uos.de</a>.</p>
          <p>Noch einmal vielen Dank für deine Teilnahme!</p>
        </div>
      </Slide>
    </Screen>

    <DebugResultsScreen v-else />
    
  </Experiment>
</template>

<script>
export default {
  name: 'App',
  methods: {
    async submit(cb) {
      await this.$magpie.submit();
      cb();
    }
  }
};
</script>
<style>
.header {
  background-image: url("../public/UOS-Logo_RotFond_sRGB_v01.jpg"), url("../public/logo_ub_2021.png");
  background-repeat: no-repeat;
  background-size: contain;
  background-position: left top, right top;
  text-align: left;
  height: 64px;
  width: auto;
  margin-bottom: 20px;
}
.fin {
  width: 60%; 
  margin: auto;
}
</style>