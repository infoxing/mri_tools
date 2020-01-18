<template>
  <mu-list textline="three-line">
  <mu-list-item  :ripple="false">
    <mu-list-item-content>
      <mu-list-item-title>Diagnostic</mu-list-item-title>
      <mu-list-item-sub-title>
        {{$store.state.patient.diagnostic}}
      </mu-list-item-sub-title>
    </mu-list-item-content>
  </mu-list-item>
  <mu-divider></mu-divider>

  <mu-list-item  :ripple="false">
    <mu-list-item-content>
      <mu-list-item-title>Allergy History</mu-list-item-title>
      <mu-list-item-sub-title>
        {{$store.state.patient.allergyHistory}}
      </mu-list-item-sub-title>
    </mu-list-item-content>
  </mu-list-item>
  <mu-divider></mu-divider>

  <mu-list-item  :ripple="false">
    <mu-list-item-content>
      <mu-list-item-title>Doctor Advice</mu-list-item-title>
      <mu-list-item-sub-title>
        {{$store.state.patient.doctorAdvice}}
      </mu-list-item-sub-title>
    </mu-list-item-content>
  </mu-list-item>
  <mu-divider></mu-divider>

  <mu-list-item  :ripple="false">
    <mu-list-item-content>
      <mu-list-item-title>Note</mu-list-item-title>
      <mu-list-item-sub-title>
        <span style="color: red;">{{$store.state.patient.note}}</span>
      </mu-list-item-sub-title>
    </mu-list-item-content>
  </mu-list-item>

</mu-list>
</template>

<script>
export default {
  name: 'PatientInformation',
  data(){return{}},
  props: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
