<template>
  <div>

    <div class="row">
      <div class=" col-xl-4" v-for="stats in statsCards" :key="stats.title">
        <!-- {{moisture.moisture}} -->
        <stats-card>
          <div v-if ="moisture.moisture[0] > 15300 && moisture.moisture[0] < 23000" class="icon-big text-center" :class="`icon-danger` " slot="header">
            <i :class="stats.icon"></i> </div>
          <div v-if ="moisture.moisture[0] > 7700 && moisture.moisture[0] < 15300" class="icon-big text-center" :class="`icon-warning` " slot="header">
            <i :class="stats.icon"></i> </div>
          <div v-if ="moisture.moisture[0] < 7700"class="icon-big text-center" :class="`icon-success` " slot="header">
            <i :class="stats.icon"></i> </div>
          <div class="numbers" slot="content">
            {{stats.title}}
            <p>สถานะ : <span v-if ="moisture.moisture[0] > 15300 && moisture.moisture[0] < 23000">น้ำยาหมด</span>
            <span v-if ="moisture.moisture[0] > 7700 && moisture.moisture[0] < 15300">น้ำยาใกล้หมด</span>
            <span v-if ="moisture.moisture[0] < 7700">น้ำยาเต็ม</span> </p>
          </div>
        </stats-card>
      </div>
    </div>
    <div class="row">
      <div class=" col-xl-8">
          <article class="message is-info">
            <div class="message-body">
            <div class=""v-if ="login === 'admin'">
              <div class="columns" v-if ="sw === 'true'">
                <div class="column">Last maintenance:</div>
              <div class="column is-one-quarter">
                {{Last_maintenance}}
              </div>
              <div class="column"><span class="button  is-info "@click="s_w()"> Update </span></div>
              <div class="column"></div>
              </div>

              <div class="columns"  v-if ="sw === 'false'">
                <div class="column">Last maintenance:</div>
              <div class="column is-one-quarter">
                <input class="input is-info" type="text":placeholder="Last_maintenance" v-model="Last_maintenance">
              </div>
              <div class="column"><span class="button  is-info "@click="save(Last_maintenance)"> save </span>
                <span class="button  is-danger "@click="Cancle()"> Cancle </span></div>
              <div class="column"></div>
              </div>
            </div>

            <div class="columns" v-if ="login === 'user'">
              <div class="column">Last maintenance:</div>
            <div class="column is-one-quarter">
               {{Last_maintenance}}
            </div>
            <div class="column"></div>
            <div class="column"></div>
            </div>

              Status : <span v-if ="moisture.moisture[0] > 15300 && moisture.moisture[0] < 23000">น้ำยาหมด</span>
              <span v-if ="moisture.moisture[0] > 7700 && moisture.moisture[0] < 15300">น้ำยาใกล้หมด</span>
              <span v-if ="moisture.moisture[0] < 7700">น้ำยาเต็ม</span>


            </br></br>
              Temp :  {{message.Temperature}} C </br></br>
              Humid :  {{message.Humidity}} % </br></br>
              Battery : 80% </br></br>
              <span v-if = "item === 'yes'" >
                <div class="buttons has-addons" v-if ="Sportlight === '1'">
                    Sportlight &nbsp;&nbsp;&nbsp;
                  <span class="button is-info" @click="Sportlight1()" >Yes</span>
                  <span class="button "@click="Sportlight1()" >No</span>
                </div>
                <div class="buttons has-addons" v-if ="Sportlight === '0'">
                    Sportlight &nbsp;&nbsp;&nbsp;
                  <span class="button"@click="Sportlight1()" >Yes</span>
                  <span class="button is-danger is-selected"@click="Sportlight1()" >No</span>
                </div>

                <div class="buttons has-addons" v-if ="GunSound === '1'">
                    GunSound &nbsp;&nbsp;&nbsp;
                  <span class="button is-info" @click="GunSound1()" >Yes</span>
                  <span class="button "@click="GunSound1()" >No</span>
                </div>
                <div class="buttons has-addons" v-if ="GunSound === '0'">
                    GunSound &nbsp;&nbsp;&nbsp;
                  <span class="button"@click="GunSound1()" >Yes</span>
                  <span class="button is-danger is-selected"@click="GunSound1()" >No</span>
                </div>

                <div class="buttons has-addons" v-if ="GunCheck === '1'">
                    GunSound &nbsp;&nbsp;&nbsp;
                  <span class="button is-info" @click="GunCheck1()" >Yes</span>
                  <span class="button "@click="GunCheck1()" >No</span>
                </div>
                <div class="buttons has-addons" v-if ="GunCheck === '0'">
                    GunCheck &nbsp;&nbsp;&nbsp;
                  <span class="button"@click="GunCheck1()" >Yes</span>
                  <span class="button is-danger is-selected"@click="GunCheck1()" >No</span>
                </div>
              </span>
            </br></br>
            </div>
          </article>
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
  /**
   * Chart data used to render stats, charts. Should be replaced with server data
   */
  data() {
    return {
      statsCards: [
        {
          type: "success",
          icon: "ti-twitter-alt",
          title: "ตู้ ATM FITM",
          value: "ปกติ"
        }
      ],
      moisture: '',
      message: '',
      login: '',
      sw: 'true',
      Last_maintenance: '',
      item: '',
      GunCheck: '',
      GunSound: '',
      Sportlight: ''
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      firebase.database().ref('/message/').once('value').then(function (snapshot) {
        that.message = snapshot.val()
      })
      firebase.database().ref('/moisture:/').once('value').then(function (snapshot) {
        that.moisture = snapshot.val()
      })
      firebase.database().ref('/login/').once('value').then(function (snapshot) {
        that.login = snapshot.val()
      })
      firebase.database().ref('/Last_maintenance/').once('value').then(function (snapshot) {
        that.Last_maintenance = snapshot.val()
      })
      firebase.database().ref('/item/').once('value').then(function (snapshot) {
        that.item = snapshot.val()
      })
      firebase.database().ref('location/atm').once('value').then(function (snapshot) {
        that.GunCheck = snapshot.val()
        that.GunSound = snapshot.val()
        that.Sportlight = snapshot.val()
        that.GunCheck = that.GunCheck.GunCheck
        that.GunSound = that.GunSound.GunSound
        that.Sportlight = that.Sportlight.Sportlight
      })
    },
    s_w () {
      this.sw = 'false'
    },
    Cancle () {
      this.sw = 'true'
    },
    save (Last_maintenance) {
      firebase.database().ref('Last_maintenance').set(Last_maintenance)
      this.Last_maintenance = ''
      this.sw = 'true'
      this.pullData()
    },
    GunCheck1 () {
      console.log('sd');
      if (this.GunCheck === '1') {
        this.GunCheck = '0'
        var data = {
          GunCheck: '0'
        }
        firebase.database().ref('location/atm').update({
          GunCheck: '0'
        })
      } else {
        this.GunCheck = '1'
        var data = {
          GunCheck: '1'
        }
        firebase.database().ref('location/atm').update({
          GunCheck: '1'
        })
      }
    },
    GunSound1 () {
      if (this.GunSound === '1') {
        this.GunSound = '0'
        var data = {
          GunSound: '0'
        }
        firebase.database().ref('location/atm').update({
          GunSound: '0'
        })
        // firebase.database().ref('location/atm').set(data)
        this.GunSound = '0'
      } else {
        this.GunSound = '1'
        var data = {
          GunSound: '1'
        }
        firebase.database().ref('location/atm').update({
          GunSound: '1'
        })
      }
    },
    Sportlight1 () {
      if (this.Sportlight === '1') {
        this.Sportlight = '0'
        var data = {
          Sportlight: '0'
        }
        firebase.database().ref('location/atm').update({
          Sportlight: '0'
        })
        // firebase.database().ref('location/atm').set(data)
        this.Sportlight = '0'
      } else {
        this.Sportlight = '1'
        var data = {
          Sportlight: '1'
        }
        firebase.database().ref('location/atm').update({
          Sportlight: '1'
        })
      }
    }
  }
}
</script>
<style>
</style>
