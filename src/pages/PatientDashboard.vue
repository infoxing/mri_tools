<template>
<mu-card style="width: 100%;  margin: 0 auto; ">
  <mu-card-header :title="$store.state.patient.name" :sub-title="$store.state.patient.sex+' - '+$store.state.patient.age" @click="$router.push('/')">
    <mu-avatar slot="avatar">
      <img src="../assets/mustermann.jpg">
    </mu-avatar>
  </mu-card-header>

  <mu-expansion-panel :expand="panel === 'panel1'" @change="toggle('panel1')">
    <div slot="header">Patient information</div>
    <Patient-Information />
    <mu-button slot="action" flat color="primary" @click="$store.state.notImplemented=true">Add Note</mu-button>
  </mu-expansion-panel>

  <mu-expansion-panel :expand="panel === 'panel2'" @change="toggle('panel2')">
    <div slot="header">Measurement</div>
    <Measurement />
    <mu-button slot="action" flat color="primary" @click="addMeasurement=true">New Measurement</mu-button>
  </mu-expansion-panel>

  <mu-expansion-panel :expand="panel === 'panel3'" @change="toggle('panel3')">
    <div slot="header">Prescription</div>
    <Prescription />
  </mu-expansion-panel>

  <mu-dialog title="Use IoT measurement device or manual input" width="600" max-width="80%" :esc-press-close="false" :overlay-close="false" :open.sync="addMeasurement">
    <mu-select label="Measurement Object" v-model="measurementObject" full-width>
      <mu-option v-for="option,index in options" :key="option" :label="option" :value="option"></mu-option>
    </mu-select>
    <mu-text-field v-if="measurementObject=='Body Temperature'" full-width v-model="tmp" placeholder="Please input......" suffix="℃   "></mu-text-field>
    <mu-button slot="actions" flat color="primary" @click="addMeasurement=false">Cancel</mu-button>
    <mu-button slot="actions" flat color="primary" @click="addMeasurement=false">ADD</mu-button>
  </mu-dialog>
</mu-card>
</template>

<script>
import PatientInformation from "../components/PatientInformation"
import Measurement from "../components/Measurement"
import Prescription from "../components/Prescription"
export default {
  name: 'PatientDashboard',
  data() {
    return {
      panel: 'panel1',
      addMeasurement: false,
      hasError: false,
      measurementObject: null,
      tmp: null,
      options: [
        "Body Temperature",
        // "Blood Pressure",
        // "Blood Sugar",
      ]
    }
  },
  mounted() {

  },
  methods: {
    jumpTo(dst) {
      this.$router.push(dst);
    },
    toggle(panel) {
      this.panel = panel === this.panel ? '' : panel;
    }
  },
  props: {
    // msg: String
  },
  components: {
    PatientInformation,
    Measurement,
    Prescription
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.mu-scale-transition-enter-active,
.mu-scale-transition-leave-active {
  transition: transform .45s cubic-bezier(0.23, 1, 0.32, 1), opacity .45s cubic-bezier(0.23, 1, 0.32, 1);
  backface-visibility: hidden;
}

.mu-scale-transition-enter,
.mu-scale-transition-leave-active {
  transform: scale(0);
  opacity: 0;
}
</style>
