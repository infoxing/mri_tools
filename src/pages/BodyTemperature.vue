<template>
<mu-card style="width: 100%;  margin: 0 auto; ">
  <mu-card-header :title="$store.state.patient.name" :sub-title="$store.state.patient.sex+' - '+$store.state.patient.age" @click="$router.push('/')">
    <mu-avatar slot="avatar">
      <img src="../assets/mustermann.jpg">
    </mu-avatar>
  </mu-card-header>

  <mu-card-media sub-title="">
    <div id="charts" style="width:100%; height:20em; background: aliceblue; box-shadow: 0px 2px 5px 1px #888888;"></div>
    <mu-button style="float: right; margin-top: -36px;" color="primary">Add</mu-button>
  </mu-card-media>

  <mu-card-text>
    <mu-list textline="two-line">
      <div v-for="bTmp in bodyTemp">
        <mu-list-item avatar :ripple="false" button>
          <mu-list-item-content>
            <mu-list-item-title>{{bTmp[0]}}</mu-list-item-title>
            <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">{{bTmp[1]}}℃</mu-list-item-sub-title>
            <mu-list-item-sub-title>
              {{bTmp[2]}}
            </mu-list-item-sub-title>
          </mu-list-item-content>
          <mu-list-item-action>
            <mu-list-item-after-text>by {{bTmp[3]}}</mu-list-item-after-text>
            <i class="material-icons" style="color:burlywood" v-if="bTmp[1]>37.4&&bTmp[1]<38">
              error_outline
            </i>
            <i class="material-icons" style="color:red" v-if="bTmp[1]>=38">
              error_outline
            </i>
            <!-- <mu-checkbox color="yellow700" input-value="bTmp[1]>37.4" value="value1" checked-icon="star"></mu-checkbox>
            <mu-checkbox color="red" input-value="bTmp[1]>38" value="value1" checked-icon="star"></mu-checkbox> -->
          </mu-list-item-action>
        </mu-list-item>
        <mu-divider></mu-divider>
      </div>
    </mu-list>
  </mu-card-text>

</mu-card>
</template>

<script>
import echarts from "echarts";

export default {
  name: 'BodyTemperature',
  data() {
    let result = [];
    let now = new Date();
    for (let i = 10; i > -1; i--) {
      let random=Math.random();
      let from;
      if (random <0.3 ){
        from="Manual input"
      }else{
        from="Automatic measurement @"+Math.floor(Math.random() * 1000) / 1000;
      }
      result[i] = [
        new Date(now - i * 1000 * 60 * 60),
        35 + Math.floor(Math.random() * 40) / 10,
        from,
        "C.J"
      ]
    }
    return {
      bodyTemp: result,
    }
  },
  methods: {
    initCharts() {
      console.log(document.getElementById("charts"));
      let myChart = this.$echarts.init(document.getElementById("charts"));
      let option = {
        title: {
          text: 'Body Temperature',
          // subtext: 'From ExcelHome',
          // sublink: 'http://e.weibo.com/1341556070/Aj1J2x5a5'
        },
        tooltip: {
          // show: true,
          // trigger: 'axis',
          axisPointer: {
            type: 'cross',
            crossStyle: {
              color: '#999'
            }
          },
          // formatter: "{c}℃"
        },
        dataZoom: [
          // {
          //   show: true,
          //   realtime: true,
          //   type: 'slider',
          //   start: 80,
          //   end: 100,
          // },
          {
            show: true,
            realtime: true,
            type: 'inside',
            start: 80,
            end: 100,
          }
        ],
        xAxis: {
          // data: function() {
          //   let now = new Date();
          //   let result = [];
          //   for (let i = 20; i > -1; i--) {
          //     result[i] = new Date(now - i * 1000 * 60 * 60);
          //     // result[i]=new Date(now);
          //   }
          //   return result;
          // }(),
          type: 'category'
        },
        yAxis: {
          min: 35,
          max: 43,
          type: 'value',
          axisLabel: {
            formatter: '{value} ℃'
          },
        },
        series: [{
          data: this.bodyTemp,
          type: 'line',
          encode: {
            x: 0,
            y: 1,
            tooltip: 1
          }
        }]
      };
      console.log(this.bodyTemp);
      myChart.setOption(option);
    }
  },
  mounted() {
    this.initCharts();
  },
  props: {
    // msg: String
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
