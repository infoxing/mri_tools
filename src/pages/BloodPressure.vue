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
      <div v-for="bPre in BloodPre">
        <mu-list-item avatar :ripple="false" button>
          <mu-list-item-content>
            <mu-list-item-title>{{bPre[0]}}</mu-list-item-title>
            <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">{{bPre[1]}} mmHg/ {{bPre[2]}}mmHg/ {{bPre[3]}}</mu-list-item-sub-title>
            <mu-list-item-sub-title>
              {{bPre[4]}}
            </mu-list-item-sub-title>
          </mu-list-item-content>
          <mu-list-item-action>
            <mu-list-item-after-text>by {{bPre[5]}}</mu-list-item-after-text>
            <i class="material-icons" style="color:burlywood" v-if="isWarning(bPre)">
              error_outline
            </i>
            <i class="material-icons" style="color:red" v-if="isDanger(bPre)">
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
function take(n,l){
  let result=[];
  for(let i=0;i<l.length;i++){
    result.push(l[i][n]);
  }
  return result;
}
export default {
  name: 'BloodPressure',
  data() {
    let result = [];
    let now = new Date();

    for (let i = 10; i > -1; i--) {
      let random = Math.random();
      let from;
      if (random <0.3 ){
        from="Manual input"
      }else{
        from="Automatic measurement @"+Math.floor(Math.random() * 1000) / 1000;
      }
      let low=50+Math.floor(random * 60);
      result[i] = [
        new Date(now - i * 8 * 1000 * 60 * 60),
        low,
        low+20+Math.floor(random * 80),
        60+Math.floor(random * 60),
        from,
        "C.J"
      ]
    }
    return {
      BloodPre: result,
    }
  },
  methods: {
    isWarning(x){
      return !this.isDanger(x) && (x[1]<40||x[1]>80||x[2]>120||x[2]-x[1]<30||x[3]>100);
    },
    isDanger(x){
      return x[1]<30||x[1]>100||x[2]>140||x[2]-x[1]<20||x[3]>120;
    },
    initCharts() {
      console.log(document.getElementById("charts"));
      let myChart = this.$echarts.init(document.getElementById("charts"));
      let option = {
        title: {
          text: 'Blood Pressure',
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          },

        },
        legend: {
          // data: ['Blood Pressure', 'Heart Rate']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        dataZoom: {
          type: 'inside',
        },
        xAxis: {
          type: 'category',
          splitLine: {
            show: false
          },
          data: take(0,this.BloodPre)
        },
        yAxis: [{
          type: 'value',
          name: 'mmHg'
        }, {
          type: 'value',
          name: 'Puls/min',
          min:0,
          max:250,
        }],
        series: [{
            name: 'Low Pressure',
            type: 'bar',
            stack: 'Blood Pressure',
            itemStyle: {
              barBorderColor: 'rgba(0,0,0,0)',
              color: 'rgba(0,0,0,0)'
            },
            label: {
              show: true,
              position: 'insideTop',
              color: 'red'
            },

            yAxisIndex: 0,
            data: take(1,this.BloodPre)
          },
          {
            name: 'High Pressure', //'High Pressure'
            type: 'bar',
            stack: 'Blood Pressure',
            label: {
              show: true,
              position: 'top'
            },
            yAxisIndex: 0,
            data: take(2,this.BloodPre)
          },
          {
            name: 'Heart Rate',
            type: 'line',
            label: {
              show: true,
            },
            yAxisIndex: 1,
            data: take(3,this.BloodPre),
            itemStyle: {
              barBorderColor: 'rgba(0,0,0,0)',
              color: 'blue'
            },
          }
        ]
      };

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
