<template>
<mu-card style="width: 100%;  margin: 0 auto; ">
  <mu-card-header title="Myron Avatar" sub-title="sub title">
    <mu-avatar slot="avatar">
      <img src="#">
    </mu-avatar>
  </mu-card-header>
  <mu-card-media :sub-title="scannResult">
    <video id="video" width="100%" height="100%" />
  </mu-card-media>
  <mu-card-title title="Drug List" sub-title="by Dr. Who"></mu-card-title>
  <mu-card-text>
    <mu-alert color="error" delete v-if="hasError" @delete="closeAlert()" transition="mu-scale-transition">
      <mu-icon left value="warning"/> Wrong medicine!
    </mu-alert>
    <mu-list textline="two-line">
      <div v-for="drug in drugs">
        <mu-list-item avatar :ripple="false" button>
          <mu-list-item-content>
            <mu-list-item-title>{{drug.name}}</mu-list-item-title>
            <mu-list-item-sub-title style="color: rgba(0, 0, 0, .87)">{{drug.Brand}}</mu-list-item-sub-title>
            <mu-list-item-sub-title>
              {{drug.id}}
            </mu-list-item-sub-title>
          </mu-list-item-content>
          <mu-list-item-action>
            <mu-list-item-after-text>{{drug.dose}}</mu-list-item-after-text>
            <mu-checkbox color="green500" v-model="drug.checked" value="" uncheck-icon="error_outline" checked-icon="done"></mu-checkbox>
          </mu-list-item-action>

        </mu-list-item>
        <mu-divider></mu-divider>
      </div>
    </mu-list>
  </mu-card-text>
  <mu-card-actions>
    <mu-button flat>Reset</mu-button>
    <mu-button flat>Confirm</mu-button>
  </mu-card-actions>
</mu-card>
</template>

<script>
import {
  BrowserQRCodeReader
} from '@zxing/library';

export default {
  name: 'HelloWorld',
  data() {
    return {
      videoInputDevices: 0,
      drugs: [{
          id: "12345678909876543",
          name: "Dolo-Dobendan® 1,4 mg / 10 mg",
          Brand: "",
          dose: "3ml",
          checked: false,
        },
        {
          id: "12345678909876543",
          name: "Dolo-Dobendan® 1,4 mg / 10 mg",
          Brand: "",
          dose: "3ml",
          checked: true,
        },
      ],
      scannResult: "Please scan the barcode of the drugs",
      hasError: false,
    }
  },
  mounted() {
    this.startScann();

  },
  methods: {
    closeAlert () {
      this.hasError = false;
    },
    searchIsDrugOnTheList(id) {
      let f = false;
      this.drugs.forEach(function(drug) {
        if (drug.id == id) {
          drug.checked = true;
          f = true;
        }
      });
      if (f == false) {
        console.log("xxxx");
        this.hasError = true;
      }
    },
    startScann() {
      let vm = this;
      const codeReader = new BrowserQRCodeReader();
      codeReader
        .listVideoInputDevices()
        .then(videoInputDevices => {
          codeReader
            .decodeFromInputVideoDevice(videoInputDevices[vm.videoInputDevices % videoInputDevices.length].deviceId, 'video')
            .then(result => {
              vm.searchIsDrugOnTheList(result.text);
              vm.scannResult = result.text;
              console.log(result.text)
            })
            .catch(err => console.error(err));
        })
        .catch(err => console.error(err));
    },
    nextViedeoInputDevices() {
      let vm = this;
      vm.videoInputDevices++;
      vm.startScann();
    }
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
