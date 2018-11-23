<template>
  <div>
    <!-- <input type="text" name="" value="" v-model="data.type">
    <input type="text" name="" value="" v-model="data.title">
    <input type="text" name="" value="" v-model="data.value">
    <button type="button" name="button" @click="insert1()">ok</button> -->
    <!-- {{moisture.moisture[0]}} -->
    <div class="row">
      <div class="col-md-6 col-xl-6" v-for="stats in location" >
        <stats-card>
          <div class="icon-big text-center" :class="`icon-${stats.type}`" slot="header">
            <i :class="stats.icon"></i>
          </div>
          <div class="numbers" slot="content">
            {{stats.title}}
            <p>สถานะ : {{stats.value}} </p>
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
      data: {
        type: '',
        icon: 'ti-twitter-alt',
        title: '',
        value: ''
      },
      statsCards: [
        {
          type: "success",
          icon: "ti-twitter-alt",
          title: "ตู้ ATM FITM",
          value: "ปกติ"
        },
        {
          type: "warning",
          icon: "ti-twitter-alt",
          title: "ตึกศิรินทร",
          value: "น้ำยาใกล้หมด"
        },
        {
          type: "success",
          icon: "ti-twitter-alt",
          title: "ลานปาล์ม",
          value: "ปกติ"
        },
        {
          type: "danger",
          icon: "ti-twitter-alt",
          title: "ใต้หลังคา",
          value: "น้ำยาหมด"
        }
      ],
      location: '',
      moisture: '',
      data_moisture: ''
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      firebase.database().ref('/message/').on('value', function(snapshot) {
        that.message = snapshot.val()
      })
      firebase.database().ref('/location1/').on('value', function(snapshot) {
        that.location = snapshot.val()
      })
      firebase.database().ref('/moisture:/').on('value', function(snapshot) {
        that.moisture = snapshot.val()
        console.log(that.moisture.moisture[0])
        if (that.moisture.moisture[0] > 15300) {
          firebase.database().ref('location1').child('-LRtpIwqM7IPLkvAxyww').update({
            type: 'danger',
            value: 'น้ำยาหมด'
          })
        } else if (that.moisture.moisture[0] > 7700) {
          firebase.database().ref('location1').child('-LRtpIwqM7IPLkvAxyww').update({
            type: 'warning',
            value: 'น้ำใกล้ยาหมด'
          })
        } else if (that.moisture.moisture[0] < 7700) {
          firebase.database().ref('location1').child('-LRtpIwqM7IPLkvAxyww').update({
            type: 'success',
            value: 'ปกติ'
          })
        }
        // that.moisture.moisture[0]
      })
    },
    insert1 () {
      console.log('sd');
      firebase.database().ref('location1').push(this.data)
    }
  }
}
</script>
<style>
</style>
