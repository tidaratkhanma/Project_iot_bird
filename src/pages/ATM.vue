<template lang="html">
  <div class="">



<b-container class="bv-example-row">
  <b-row>
    <b-col cols="4">  <stats-card>
        <div class="icon-big text-center" :class="colorB" slot="header">
          <i class="ti-twitter-alt"></i>
        </div>
        <div class="numbers" slot="content">
          {{showsite.name_site}}
          <p>สถานะ : {{status}}  </p>
        </div>
      </stats-card>
    </b-col>
  </b-row>
</b-container>
    <div class="row">
      <div class="">
          <article class="message ">
            <div class="message-body">
              <b-card-text>
                <div class="" v-if ="login === 'admin'">
                  <div class="columns" v-if ="sw === 'true'">

                    <div class="column n is-one-third">Last maintenance:</div>
                  <div class="column is-one-third">
                    {{showsite.Last_maintenance}}
                  </div>
                  <div class="column"><span class="button  is-info " @click="s_w()"> Update </span></div>
                  <div class="column"></div>
                  </div>

                  <div class="columns"  v-if ="sw === 'false'">
                    <div class="column">Last maintenance:</div>
                  <div class="column is-one-third">
                    <input class="input is-info" type="date" :placeholder="Last_maintenance" v-model="Last_maintenance">
                  </div>
                  <div class="column">
                    <div class="row">
                      <div class="button  is-info " @click="save()"> save </div> &nbsp;&nbsp;
                      <div class="button  is-danger " @click="Cancle()"> Cancle </div>
                    </div>
                  </div>
                  </div>
                </div>

                <div class="columns" v-if ="login === 'user'">
                  <div class="column">Last maintenance:</div>
                <div class="column is-one-quarter">
                   {{showsite.Last_maintenance}}
                </div>
                <div class="column"></div>
                <div class="column"></div>
                </div>
              </b-card-text> <br>


              Temp (C):  <b-progress :value="showsite.Temperature" :max="max" show-progress animated  variant="link"/> <br>
              Humid (%):  <b-progress :value="showsite.Humidity" :max="max" show-progress animated  variant="success"/> <br>
              Battery (volt): <b-progress :value="showsite.Battery" :max="max" show-progress animated  variant="warning"/>

              <!-- <span v-if = "item === 'yes'" >
                <div class="buttons has-addons" v-if ="showsite.GunCheck === 1">
                     GunCheck &nbsp;&nbsp;&nbsp;
                   <span class="button is-info is-rounded" >Yes</span> &nbsp;&nbsp;&nbsp;
                   <span class="button is-rounded" >No</span>
                 </div>
                 <div class="buttons has-addons" v-if ="showsite.GunCheck === 0">
                     GunCheck &nbsp;&nbsp;&nbsp;
                   <span class="button  is-rounded " >Yes</span>&nbsp;&nbsp;&nbsp;
                   <span class="button is-danger is-rounded is-selected" >No</span>
                 </div>
               </span> -->
            </div>
          </article>
      </div>
    </div>
</br>
    <span v-if = "item === 'yes'" >
      <div class="columns">
        <div class="column">
          <article class="message is-warning">
        <div class="message-body">
            <div class="buttons has-addons" v-if ="showsite.Sportlight1 === '1'">
                Sportlight 1 &nbsp;&nbsp;&nbsp;
              <span class="button is-info" @click="Sportlight1('1')" >Yes</span>
              <span class="button " @click="Sportlight1('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight1 === '0'">
                Sportlight 1 &nbsp;&nbsp;&nbsp;
              <span class="button" @click="Sportlight1('1')" >Yes</span>
              <span class="button is-danger is-selected" @click="Sportlight1('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight2 === '1'">
                Sportlight 2 &nbsp;&nbsp;&nbsp;
              <span class="button is-info" @click="Sportlight2('1')" >Yes</span>
              <span class="button " @click="Sportlight2('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight2 === '0'">
                Sportlight 2 &nbsp;&nbsp;&nbsp;
              <span class="button" @click="Sportlight2('1')" >Yes</span>
              <span class="button is-danger is-selected" @click="Sportlight2('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight3 === '1'">
                Sportlight 3 &nbsp;&nbsp;&nbsp;
              <span class="button is-info" @click="Sportlight3('1')" >Yes</span>
              <span class="button " @click="Sportlight3('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight3 === '0'">
                Sportlight 3 &nbsp;&nbsp;&nbsp;
              <span class="button" @click="Sportlight3('1')" >Yes</span>
              <span class="button is-danger is-selected" @click="Sportlight3('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight4 === '1'">
                Sportlight 4 &nbsp;&nbsp;&nbsp;
              <span class="button is-info" @click="Sportlight4('1')" >Yes</span>
              <span class="button " @click="Sportlight4('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight4 === '0'">
                Sportlight 4 &nbsp;&nbsp;&nbsp;
              <span class="button" @click="Sportlight4('1')" >Yes</span>
              <span class="button is-danger is-selected" @click="Sportlight4('0')" >No</span>
            </div>

        </div>
      </article>
        </div>
        <div class="column">
          <article class="message is-warning">
        <div class="message-body">
          <div class="buttons has-addons" v-if ="showsite.Gunsound1 === '1'">
              GunSound 1 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound1('1')" >Yes</span>
            <span class="button " @click="GunSound1('0')" >No</span>
            <span class="button " @click="GunSound1('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound1 === '0'">
              GunSound 1 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound1('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound1('0')" >No</span>
            <span class="button " @click="GunSound1('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound1 === '2'">
              GunSound 1 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound1('1')" >Yes</span>
            <span class="button" @click="GunSound1('0')" >No</span>
            <span class="button is-success is-selected" @click="GunSound1('2')" >Auto</span>
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '1'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound2('1')" >Yes</span>
            <span class="button " @click="GunSound2('0')" >No</span>
            <span class="button " @click="GunSound2('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '0'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound2('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound2('0')" >No</span>
            <span class="button " @click="GunSound2('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '2'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound2('1')" >Yes</span>
            <span class="button" @click="GunSound2('0')" >No</span>
            <span class="button is-success is-selected" @click="GunSound2('2')" >Auto</span>
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '1'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound3('1')" >Yes</span>
            <span class="button " @click="GunSound3('0')" >No</span>
            <span class="button " @click="GunSound3('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '0'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound3('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound3('0')" >No</span>
            <span class="button " @click="GunSound3('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '2'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound3('1')" >Yes</span>
            <span class="button" @click="GunSound3('0')" >No</span>
            <span class="button is-success is-selected" @click="GunSound3('2')" >Auto</span>
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '1'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound4('1')" >Yes</span>
            <span class="button " @click="GunSound4('0')" >No</span>
            <span class="button " @click="GunSound4('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '0'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound4('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound4('0')" >No</span>
            <span class="button " @click="GunSound4('2')" >auto</span>
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '2'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound4('1')" >Yes</span>
            <span class="button" @click="GunSound4('0')" >No</span>
            <span class="button is-success is-selected" @click="GunSound4('2')" >Auto</span>
          </div>
        </div>
      </article>
        </div>
      </div>
    </span>

    <chart-card
                :chart-data="activityChart.data"
                :chart-options="activityChart.options">
      <span slot="footer">
        <a class="button is-info  is-focused">show report</a>
      </span>
      <div slot="legend">
        <i class="fa fa-circle text-info"></i> นกพิราบ
        <i class="fa fa-circle text-warning"></i> นกกระจอก
      </div>
    </chart-card>

    <chart-card title=""
                sub-title=""
                :chart-data="usersChart.data"
                :chart-options="usersChart.options">
      <span slot="footer">
        <i class="ti-reload"></i> Updated 3 minutes ago
      </span>
      <div slot="legend">
        <i class="fa fa-circle text-info"></i> Open
        <i class="fa fa-circle text-danger"></i> Click
        <i class="fa fa-circle text-warning"></i> Click Second Time
      </div>
    </chart-card>
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
        max: 100,
     Site: '',
     activeSite: '',
     showsite: '',
     colorB: '',
     status: '',
     login: '',
     sw: 'true',
     Last_maintenance: '',
     item: '',
     login: '',
     active: '',
     activityChart: {
       data: {
         labels: [
           "19/11/61",
           "20/11/61",
           "21/11/61",
           "22/11/61",
           "23/11/61",
           "24/11/61",
           "25/11/61",
           "26/11/61",
           "27/11/61",
           "28/11/61",
           "29/11/61",
           "30/11/61"
         ],
         series: [
           [5, 10, 15, 20, 25, 30, 35, 5, 9, 25, 8, 1],
           [1, 27, 34, 13, 6, 33, 19, 38, 10, 15, 11, 25]
         ]
       },
       options: {
         seriesBarDistance: 10,
         axisX: {
           showGrid: false
         },
         height: "245px"
       }
     },
     usersChart: {
       data: {
         labels: [
           "9:00AM",
           "12:00AM",
           "3:00PM",
           "6:00PM",
           "9:00PM",
           "12:00PM",
           "3:00AM",
           "6:00AM"
         ],
         series: [
           [287, 385, 490, 562, 594, 626, 698, 895, 952],
           [67, 152, 193, 240, 387, 435, 535, 642, 744],
           [23, 113, 67, 108, 190, 239, 307, 410, 410]
         ]
       },
       options: {
         low: 0,
         high: 1000,
         showArea: true,
         height: "245px",
         axisX: {
           showGrid: false
         },
         lineSmooth: Chartist.Interpolation.simple({
           divisor: 3
         }),
         showLine: true,
         showPoint: false
       }
     }
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
      firebase.database().ref('/activeSite/').on('value', function(snapshot) {
         that.activeSite = snapshot.val()
         that.site()
       })
       firebase.database().ref('/active/').on('value', function(snapshot) {
        that.active = snapshot.val()
        that.site()
      })
       firebase.database().ref('/login/').on('value', function(snapshot) {
         that.login = snapshot.val()
         that.site()
       })
       firebase.database().ref('/member/').on('value', function(snapshot) {
         that.item = snapshot.val()
         that.site()
       })


    },
    site () {
      // alert('zxfsff')
      for (var variable in this.Site) {
        if (this.activeSite === variable) {
          this.showsite = this.Site[variable]
            // this.colorB = 'icon-success'
          if (this.showsite.moisture<7700) {
            this.colorB = 'icon-success'
            this.status = 'ปกติ'
          } else if (this.showsite.moisture<15300) {
            this.colorB = 'icon-warning'
            this.status = 'น้ำยาใกล้หมด'
          } else if (this.showsite.moisture>15300) {
            this.colorB = 'icon-danger'
            this.status = 'น้ำยาหมด'
          }
        }
      }
      for (var variable in this.item) {
        console.log(this.active)
        if (this.active === this.item[variable].username) {
          this.item = this.item[variable].item
          console.log(this.item[variable].item);
        }
      }
    },
    s_w () {
      this.sw = 'false'
    },
    Cancle () {
      this.sw = 'true'
    },
    save () {
      firebase.database().ref('Site').child(this.activeSite).update({
        Last_maintenance: this.Last_maintenance
      })
      this.Last_maintenance = ''
      this.sw = 'true'
      this.pullData()
    },
    Sportlight1 (data) {
      console.log('data '+ data);
      firebase.database().ref('Site').child(this.activeSite).update({
        Sportlight1: data
      })
      this.pullData()
    },
    Sportlight2 (data) {
      console.log('data '+ data);
      firebase.database().ref('Site').child(this.activeSite).update({
        Sportlight2: data
      })
      this.pullData()
    },
    Sportlight3 (data) {
      console.log('data '+ data);
      firebase.database().ref('Site').child(this.activeSite).update({
        Sportlight3: data
      })
      this.pullData()
    },
    Sportlight4 (data) {
      console.log('data '+ data);
      firebase.database().ref('Site').child(this.activeSite).update({
        Sportlight4: data
      })
      this.pullData()
    },
    GunSound1 (data) {
      firebase.database().ref('Site').child(this.activeSite).update({
        Gunsound1: data
      })
      this.pullData()
    },
    GunSound2 (data) {
      firebase.database().ref('Site').child(this.activeSite).update({
        Gunsound2: data
      })
      this.pullData()
    },
    GunSound3 (data) {
      firebase.database().ref('Site').child(this.activeSite).update({
        Gunsound3: data
      })
      this.pullData()
    },
    GunSound4 (data) {
      firebase.database().ref('Site').child(this.activeSite).update({
        Gunsound4: data
      })
      this.pullData()
    }
  }
}
</script>

<style lang="css">

.sc-gauge  { width:200px; height:200px; text-align:center ;}
.sc-background { position:relative; height:100px; margin-bottom:10px; background-color:#fff; border-radius:150px 150px 0 0; overflow:hidden; text-align:center; }
.sc-mask { position:absolute; top:20px; right:20px; left:20px; height:80px; background-color:#f4f3ef; border-radius:150px 150px 0 0 }
.sc-percentage { position:absolute; top:100px; left:-200%; width:400%; height:400%; margin-left:100px; background-color:#00aeef; }
.sc-percentage { transform:rotate(158deg); transform-origin:top center; }
.sc-min { float:left; }
.sc-max { float:right; }
.sc-value { position:absolute; top:50%; left:0; width:100%;  font-size:48px; font-weight:700 }
</style>
