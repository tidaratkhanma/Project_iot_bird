<template>
  <div>
    <div class="row">
      <div class="col-md-6 col-xl-6" v-for = "(site,key) in Site"  @click="atcive(key)" >
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
            <p v-else-if = "site.moisture<15300 ">สถานะ : น้ำยาใกล้หมด  </p>
            <p v-else-if = "site.moisture>15300 ">สถานะ : น้ำยาหมด </p>
        </div>
        </stats-card>
      </div>
    </div>
    <!-- <div class="col-md-6 col-xl-6" v-for = "(site,key) in Site"  @click="atcive(key)" >
    <p v-if = "site.moisture<7700 ">สถานะ : ปกติ  </p>
    <p v-else-if = "site.moisture<15300 ">สถานะ : น้ำยาใกล้หมด  </p>
    <p v-else-if = "site.moisture>15300 ">สถานะ : {{num}} </p> -->

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
      colorB: 'icon-success',
      num: 0
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
        for(var a  in that.Site) {
          if(that.Site[a].moisture > 15300) {
            that.num = that.num + 1
          }
        }
    },
    site () {
      // alert('zxfsff')
      for (var variable in this.Site) {
        if (this.activeSite === variable) {
          this.showsite = this.Site[variable]
            // this.colorB = 'icon-success'
        }
      }
    },
    atcive (key) {
      // alert(key)
        this.$router.replace('/ATM/' + key)
      firebase.database().ref('activeSite').set(key)
    }
  }
}
</script>
<style>
</style>
