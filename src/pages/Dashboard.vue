<template>
  <div>
    <div class="row">
      <div class="col-md-6 col-xl-6" v-for = "site in Site" >
        <stats-card>
          <div v-if = "site.moisture<7700" class="icon-big text-center" :class="'icon-success'" slot="header">
             <i class="ti-twitter-alt"></i>
          </div>
          <div v-else-if = "site.moisture<15300" class="icon-big text-center" :class="'icon-warning'" slot="header">
             <i class="ti-twitter-alt"></i>
          </div>
          <div v-else-if = "site.moisture>15300" class="icon-big text-center" :class="'icon-danger'" slot="header">
             <i class="ti-twitter-alt"></i>
          </div>
        <div class="numbers" slot="content">
        {{site.name_site}}
          <p v-if = "site.moisture<7700 ">สถานะ : ปกติ  </p>
            <p v-else-if = "site.moisture<15300 ">สถานะ :น้ำยาใกล้หมด  </p>
            <p v-else-if = "site.moisture>15300 ">สถานะ : น้ำยาหมด </p>
        </div>
        </stats-card>
      </div>
    </div>
  </div>
</template>
<script>
import { StatsCard, ChartCard } from "@/components/index";
import Chartist from 'chartist';
import firebase from 'firebase'
export default {
  components: {
    StatsCard,
    ChartCard
  },
  data() {
    return {
      Site: '',
      colorB: 'icon-success'
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      firebase.database().ref('/Site/').on('value', function(snapshot) {
         that.Site = snapshot.val()
         that.site()
        })
    },
    site () {
      // alert('zxfsff')
      for (var variable in this.Site) {
        if (this.activeSite === variable) {
          this.showsite = this.Site[variable]
            // this.colorB = 'icon-success'

        }
      }
    }
  }
}
</script>
<style>
</style>
