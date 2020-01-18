<template>
  <mu-list textline="three-line">
      <mu-list-item :ripple="false" button @click="jumpTo('/drugsChecker')">
        <mu-list-item-content>
          <mu-list-item-title>Injection</mu-list-item-title>
          <!-- <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">Brunch this weekend?</mu-list-item-sub-title> -->
          <mu-list-item-sub-title>
            Saline
          </br>
            Levaquin
          </br>
            ...
          </mu-list-item-sub-title>
        </mu-list-item-content>
        <mu-list-item-action >
          <mu-list-item-after-text>15 min ago</mu-list-item-after-text>
          <span style="">waiting</span>
        </mu-list-item-action>
      </mu-list-item>
      <mu-divider></mu-divider>

      <mu-list-item :ripple="false" button @click="jumpTo('/drugsChecker')">
        <mu-list-item-content>
          <mu-list-item-title>Take Medicine</mu-list-item-title>
          <!-- <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">high / Low pressure / Heart rate</mu-list-item-sub-title> -->
          <mu-list-item-sub-title>
            VITAMIN D3 HEVERT® 4000 IE </br>
            ADDITIVA® Vitamin C + Zink Depot 300 mg Kapseln
          </mu-list-item-sub-title>
        </mu-list-item-content>
        <mu-list-item-action >
          <mu-list-item-after-text>4 hr ago</mu-list-item-after-text>
          <mu-checkbox color="green500" v-model="bTOK" value="value3"  uncheck-icon="error_outline" checked-icon="check_circle_outline"></mu-checkbox>
        </mu-list-item-action>
      </mu-list-item>
      <mu-divider></mu-divider>
       <mu-list-item :ripple="false" button >
        <mu-list-item-content>
          <mu-list-item-title>Food Delivery</mu-list-item-title>
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
  methods:{
    jumpTo(dst){
      this.$router.push(dst);
    },
  },
  props: {

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
