<template>
  <mu-list textline="two-line">
      <mu-list-item avatar :ripple="false" button @click="$router.push('/bodyTemperature')">
        <mu-list-item-content>
          <mu-list-item-title>Body Temperature</mu-list-item-title>
          <!-- <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">Brunch this weekend?</mu-list-item-sub-title> -->
          <mu-list-item-sub-title>
            36.8 ℃
          </mu-list-item-sub-title>
        </mu-list-item-content>
        <mu-list-item-action >
          <mu-list-item-after-text>15 min ago</mu-list-item-after-text>
          <mu-checkbox color="green500" v-model="bTOK" value="value1" uncheck-icon="error_outline" checked-icon="check_circle_outline"></mu-checkbox>
        </mu-list-item-action>
      </mu-list-item>
      <mu-divider></mu-divider>

      <mu-list-item avatar :ripple="false" button @click="$router.push('/bloodPressure')">
        <mu-list-item-content>
          <mu-list-item-title>Blood Pressure</mu-list-item-title>
          <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">high / Low pressure / Heart rate</mu-list-item-sub-title>
          <mu-list-item-sub-title>
            <span style="color:red">148 mmHg</span>
            <span> / </span>
            <span style="color:burlywood">87 mmHg</span>
            <span> / </span>
            <span >78</span>
          </mu-list-item-sub-title>
        </mu-list-item-content>
        <mu-list-item-action >
          <mu-list-item-after-text>4 hr ago</mu-list-item-after-text>
          <mu-checkbox color="yellow700" v-model="bTOK" value="value2"  uncheck-icon="star_border" checked-icon="error_outline"></mu-checkbox>
        </mu-list-item-action>
      </mu-list-item>
      <mu-divider></mu-divider>
       <mu-list-item avatar :ripple="false" button>
        <mu-list-item-content>
          <mu-list-item-title>Blood Sugar</mu-list-item-title>
          <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">Oui oui</mu-list-item-sub-title>
          <mu-list-item-sub-title>
            Do you have Paris recommendations? Have you ever been?
          </mu-list-item-sub-title>
        </mu-list-item-content>
        <mu-list-item-action >
          <mu-list-item-after-text>6 hr</mu-list-item-after-text>
          <mu-checkbox color="green500" v-model="bTOK" value="value3"  uncheck-icon="error_outline" checked-icon="check_circle_outline"></mu-checkbox>
        </mu-list-item-action>
      </mu-list-item>
    </mu-list>
</template>

<script>
export default {
  name: 'Measurement',
  data(){
    return {
      bTOK:true,

    }
  },
  props: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
