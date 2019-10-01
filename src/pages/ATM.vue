<template lang="html">
  <div class="">

 <a class="button is-danger" style ="float: right;" @click="dash('/dashboard')">
    <span class="icon is-small">
      <i class="fas fa-times"></i>
    </span>
  </a><br><br><br>
<b-container class="bv-example-row">
  <div class="columns is-desktop">
  <div class="column is-two-fifths ">
    <stats-card>
           <div class="icon-big text-center" :class="colorB" slot="header">
             <i class="ti-twitter-alt"></i>
           </div>
           <div class="numbers" slot="content">
             {{showsite.name_site}}
             <p>สถานะ : {{status}}  </p>
           </div>
   </stats-card>
  </div>
  <div class="column"  v-if = "status1 === 'false'">
    <b-container class="bv-example-row">
      <b-row>
        <b-col>  <img  v-if = " Detection.Detection1 === '1' " src="../assets/img/bird.png" width="95%" ></b-col>
        <b-col> <img    v-if = "  Detection.Detection2 === '1'" src="../assets/img/bird.png" width="95%"></b-col>
        <b-col> <img  v-if = "   Detection.Detection3 === '1'" src="../assets/img/bird.png" width="95%"></b-col>
        <b-col>  <img    v-if = "  Detection.Detection4 === '1'" src="../assets/img/bird.png" width="95%"></b-col>
      </b-row>
    </b-container>

  </div>
  <!-- <div class="column"></div> -->
</div>
</b-container> <br>
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
                  <div class="column"><span class="button  is-primary " @click="s_d()"> Show detail </span></div>
                  </div>
                  <div v-if="detail === 't'">
                    สถิติการเติมน้ำยา </br>
                    <span v-for ="a in data_detail"> {{a.day}}  </br> </span>
                  </div>
                  <div class="columns"  v-if ="sw === 'false'">
                    <div class="column">Last maintenance:</div>
                  <div class="column is-one-third">
                    <input class="input is-info" type="date" :placeholder="Last_maintenance" v-model="Last_maintenance">
                  </div>
                  <div class="column">
                    <div class="row">
                      <div class="button  is-info " @click="save(showsite.num_day, showsite.Last_maintenance)"> save </div> &nbsp;&nbsp;
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
              <!-- Battery (volt): <b-progress :value="showsite.Battery" :max="max" show-progress animated  variant="warning"/> -->
            </div>
          </article>
</br>
<!-- {{status}} -->

    <span v-if = "item === 'yes'" >
      <div v-if = "activeSite == '-Lhmrm7IPud9uCvblIfA'" >
      <div class="columns" v-if = "">
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
              <span class="button is-info"  @click="Sportlight4('1')" >Yes</span>
              <span class="button "  @click="Sportlight4('0')" >No</span>
            </div>
            <div class="buttons has-addons" v-if ="showsite.Sportlight4 === '0'">
                Sportlight 4 &nbsp;&nbsp;&nbsp;
              <span class="button"  @click="Sportlight4('1')" >Yes</span>
              <span class="button is-danger is-selected"  @click="Sportlight4('0')" >No</span>
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
            <!-- <span class="button " @click="GunSound1('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound1 === '0'">
              GunSound 1 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound1('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound1('0')" >No</span>
            <!-- <span class="button " @click="GunSound1('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound1 === '2'">
              GunSound 1 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound1('1')" >Yes</span>
            <span class="button" @click="GunSound1('0')" >No</span>
            <!-- <span class="button is-success is-selected" @click="GunSound1('2')" >Auto</span> -->
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '1'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound2('1')" >Yes</span>
            <span class="button " @click="GunSound2('0')" >No</span>
            <!-- <span class="button " @click="GunSound2('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '0'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound2('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound2('0')" >No</span>
            <!-- <span class="button " @click="GunSound2('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound2 === '2'">
              GunSound 2 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound2('1')" >Yes</span>
            <span class="button" @click="GunSound2('0')" >No</span>
            <!-- <span class="button is-success is-selected" @click="GunSound2('2')" >Auto</span> -->
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '1'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button is-info" @click="GunSound3('1')" >Yes</span>
            <span class="button " @click="GunSound3('0')" >No</span>
            <!-- <span class="button " @click="GunSound3('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '0'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound3('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound3('0')" >No</span>
            <!-- <span class="button " @click="GunSound3('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound3 === '2'">
              GunSound 3 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound3('1')" >Yes</span>
            <span class="button" @click="GunSound3('0')" >No</span>
            <!-- <span class="button is-success is-selected" @click="GunSound3('2')" >Auto</span> -->
          </div>

          <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '1'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button is-info"  @click="GunSound4('1')" >Yes</span>
            <span class="button " @click="GunSound4('0')" >No</span>
            <!-- <span class="button " @click="GunSound4('2')" >auto</span> -->
          </div>
          <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '0'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button"  @click="GunSound4('1')" >Yes</span>
            <span class="button is-danger is-selected" @click="GunSound4('0')" >No</span>
            <!-- <span class="button " @click="GunSound4('2')" >auto</span> -->
          </div>
          <!-- <div class="buttons has-addons" v-if ="showsite.Gunsound4 === '2'">
              GunSound 4 &nbsp;&nbsp;&nbsp;
            <span class="button" @click="GunSound4('1')" >Yes</span>
            <span class="button" @click="GunSound4('0')" >No</span>
            <span class="button is-success is-selected" @click="GunSound4('2')" >Auto</span>
          </div> -->
        </div>
      </article>
        </div>
      </div>
      </div>
    </span>
    <br>
 <br>
<b>สภาพแวดล้อมที่มีผลต่อการละเหยของน้ำยา </b>  <br>  <br>
    <chart-card title=""
                :chart-data="activityChart.data"
                :chart-options="activityChart.options">
      <span slot="footer">
          <!-- <a class="button is-danger  is-focused" v-if="show === 't'" @click="sw_show('f')">close  report</a>
        <a class="button is-info  is-focused" v-if="show === 'f'"  @click="sw_show('t')">show report</a> -->
      </span>
      <div slot="legend">
        <i class="fa fa-circle text-info"></i> ระดับน้ำยา
        <i class="fa fa-circle text-warning"></i> อุญหภูมิ
        <i class="fa fa-circle text-danger"></i> ความชื้น
      </div>
    </chart-card>
<div v-if="show === 't'">

    <div class="columns is-mobile">
      <div class="column  is-one-fifth">
        <br>
        ****<br>
        อัตตราการลดลงของ moisture ที่มีผลมาจาก Temperature<br>
        Temperature 10 C ลดลง  9.3<br>
        Temperature 20 C ลดลง  17.5<br>
        Temperature 30 C ลดลง  30.5<br>
        Temperature 40 C ลดลง  40.5<br>
      </div>
      <div class="column">
        <table>
          <tr>
            date
          </tr>
        <div v-for ="a in activityChart.data.labels">
          <tr> {{a}} </tr>
        </div>
      </table>
      </div>

  <div class="column">
    <table>
      <tr>
        Temperature
      </tr>
      <div v-for ="a in tem">
          <tr> {{a}} องศา</tr>
      </div>
  </table>
  </div>
  <div class="column">
    <table>
      <tr>
        moisture
      </tr>
    <div v-for ="a in mo">
      <tr> {{a}} %</tr>
    </div>
  </table>
  </div>
  <div class="column">
    <table>
      <tr>
        Humidity
      </tr>
    <div v-for ="a in hu">
      <tr> {{a}} %</tr>
    </div>
  </table>
  </div>

</div>
</div>
<br>
<div v-if = "activeSite == '-Lhmrm7IPud9uCvblIfA'">
  <div>
  <b-button v-b-toggle.collapse-1 variant="primary">สถิตินก</b-button>
  <b-collapse id="collapse-1" class="mt-2">
    <b-card>
    <table>
      <tr>
        <td>วันที่</td>
        <td>จำนวนนก</td>
          <td>จำนวนนกที่เพิ่มขึ้น</td>
          <td>จำนวนนกที่ลดลง</td>

      </tr>
      <tr v-for="date in dated">
        <td > {{date.substring(0,9)}}   </td>
        <td>{{Site[activeSite][date.substring(3, 6)][date.substring(0, 2)]}}</td>
        <td v-if="parseInt(date.substring(0,2),10)-1 == 0">0</td>
        <td v-else-if="parseInt(date.substring(0,2),10) < 10">{{(Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10))] > Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)])?Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10))] - Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)]:'0'}}</td>
        <td v-else-if="parseInt(date.substring(0,2),10) >= 10 && (parseInt(date.substring(0,2),10))-1 == 9">{{(Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)] < Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)])?Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)] - Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)]:'0'}}</td>
        <td v-else-if="parseInt(date.substring(0,2),10) >= 10 && (parseInt(date.substring(0,2),10))-1 > 9">{{(Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)-1] < Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)])?Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)] - Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)-1]:'0'}}</td>
        <td v-if="parseInt(date.substring(0,2),10)-1 == 0">0</td>
        <td v-else-if="parseInt(date.substring(0,2),10) < 10">{{(Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10))] < Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)])?Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)] - Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10))]:'0'}}</td>
        <td v-else-if="parseInt(date.substring(0,2),10) >= 10 && (parseInt(date.substring(0,2),10))-1 == 9">{{(Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)] > Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)])?Site[activeSite][date.substring(3, 6)]['0'+''+(parseInt(date.substring(0,2),10)-1)] - Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)]:'0'}}</td>
        <td v-else-if="parseInt(date.substring(0,2),10) >= 10 && (parseInt(date.substring(0,2),10))-1 > 9">{{(Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)-1] > Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)])?Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)-1] - Site[activeSite][date.substring(3, 6)][parseInt(date.substring(0,2),10)]:'0'}}</td>
      </tr>
    </table>
    </b-card>
  </b-collapse>
</div>
<br><br>
จำนวนนกทั้งหมด  {{Detection.total}} ตัว <span class="button is-rounded  is-primary " @click="reset('all')"> reset all </span>
<div class="columns">
  <div class="column">
  </div>
  <div class="column">
    <center> จำนวนนก {{Detection.total2}} ตัว <br> <span class="button is-rounded  is-primary " @click="reset('2')"> reset </span>
    </center>
  </div>
  <div class="column">
  </div>
</div>


<div class="columns">
  <div class="column"><br><br><br><br><br><br>
  <center>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
     จำนวนนก {{Detection.total1}} ตัว <br>
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
     &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
     <span class="button is-rounded  is-primary " @click="reset('1')"> reset </span>
  </center>
  </div>
  <div class="column">
    <img src="../assets/image.png">

  </div>
  <div class="column"><br><br><br><br><br><br>
  <left>&nbsp;&nbsp;&nbsp;&nbsp;  จำนวนนก {{Detection.total3}} ตัว</left><br>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
  <span class="button is-rounded  is-primary " @click="reset('3')"> reset </span>
  </div>
</div>


<div class="columns">
  <div class="column">
  </div>
  <div class="column">
  <center>  จำนวนนก   {{Detection.total4}} ตัว <br><span class="button is-rounded  is-primary " @click="reset('4')"> reset </span></center>
  </div>
  <div class="column">
  </div>
</div>
</div>
<br>
<article class="message is-link">
  <div class="message-body">
      <strong></strong>  <br>
    <strong>ระยะเวลาที่น้ำยาสามารถอยู่ได้ต่อการเติมแต่ละครั้ง :</strong> {{showsite.day_moisture}} วัน   <span class="button  is-primary " @click="reset('day')"> reset  </span><br>
    <strong>สถิติการเติมน้ำยา :</strong> {{showsite.num_day}} ครั้ง/เดือน   <span class="button is-primary " @click="reset('month')"> reset  </span><br>

  </div>
</article>
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
     status1: '',
     detail: 'f',
     tem: [],
     mo: [],
     hu: [],
     Detection: '',
     show: 'f',
     max:  100,
     Site: '',
     activeSite: '',
     showsite: '',
     colorB: '',
     status: '',
     login: '',
     sw: 'true',
     Last_maintenance: '',
     datee_maintenance: '',
     item: '',
     login: '',
     active: '',
     dated: '',
     sep: '',
     oct: '',
     nov: '',
     dec: '',
     jan: '',
     feb: '',
     activityChart: {
       data: {
         labels: [],
         series: []
       },
       options: {
         seriesBarDistance: 10,
         axisX: {
           showGrid: false
         },
         height: "245px"
       }
     },
     a: [],
     data_detail: ''
   }
 },
 mounted() {
   this.pullData()
  },
 created: function () {
     this.pullData()
  },
  methods: {
    reset (data) {
      let that = this
      if (data === 'all') {
        firebase.database().ref('/Site/'+that.activeSite + '/Detection').update({
          total: 0,
          total1: 0,
          total2: 0,
          total3: 0,
          total4: 0,
        })
      }
      else if  (data === '1') {
        var a = +this.Detection.total - +this.Detection.total1
        firebase.database().ref('/Site/'+that.activeSite + '/Detection').update({
          total: a,
          total1: 0
        })
      }
      else if  (data === '2') {
        var a = +this.Detection.total - +this.Detection.total2
        firebase.database().ref('/Site/'+that.activeSite + '/Detection').update({
          total: a,
          total2: 0
        })
      }
      else if  (data === '3') {
        var a = +this.Detection.total - +this.Detection.total3
        firebase.database().ref('/Site/'+that.activeSite + '/Detection').update({
          total: a,
          total3: 0
        })
      }
      else if  (data === '4') {
        var a = +this.Detection.total - +this.Detection.total4
        firebase.database().ref('/Site/'+that.activeSite + '/Detection').update({
          total: a,
          total4: 0
        })
      }
      else if  (data === 'day') {
        firebase.database().ref('Site').child(this.activeSite).update({
          day_moisture : 0
        })
      }
      else if  (data === 'month') {
        firebase.database().ref('Site').child(this.activeSite).update({
          num_day: 0
        })
      }
      firebase.database().ref('/Site/'+that.activeSite+'/date_maintenance').remove()
    },
    dash (dash) {
      this.$router.replace(dash)
    },
    bird () {
      var total = 0
      var num = this.showsite.Detection.total
      total = this.showsite.Detection.total - num
      firebase.database().ref('Site').child(this.activeSite).update({
        num_b: total
      })
    },
    sw_show (data) {
        this.show = data
    },
    moisture () { //คำนวนอัตราการระเหยของน้ำยา
      for (var variable in this.Site) {
          var num = 0
          var data = this.showsite.Temperature
          var Humid  = this.showsite.Humidity

      if (this.Site[variable].Temperature <= 10) {
        num = this.Site[variable].moisture + 9.3
        firebase.database().ref('Site').child(variable).update({
          moisture: num
        })
        firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
        firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
       }
      else if (this.Site[variable].Temperature <= 20) {
        num = this.Site[variable].moisture + 17.5
        firebase.database().ref('Site').child(variable).update({
          moisture: num
        })
      firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
      firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
      }
      else if (this.Site[variable].Temperature <= 30) {
        num = this.Site[variable].moisture + 30.5
        firebase.database().ref('Site').child(variable).update({
          moisture: num
        })
        firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
        firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
        }
      else if (this.Site[variable].Temperature <= 40) {
          num = this.Site[variable].moisture + 40.5
          firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
          firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
        }
        else if (this.Site[variable].Temperature <= 50) {
          num = this.Site[variable].moisture + 50.5
          firebase.database().ref('Site').child(variable).update({
            moisture: num
          })
          firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
          firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
        }
        else {
          num = this.Site[variable].moisture + 60.5
          firebase.database().ref('Site').child(variable).update({
            moisture: num
          })
          firebase.database().ref('Site/'+variable + '/moisture_h').push(num)
          firebase.database().ref('Site/'+variable + '/Temperature_h').push(data)
        }
        firebase.database().ref('Site').child(variable).update({
          Temperature: data
        })
        firebase.database().ref('Site').child(variable).update({
          Humidity: Humid
        })
      }
      this.hour()
    },
    pullData () {
      let that = this
      firebase.database().ref('/Site/').on('value', function(snapshot) {
         that.Site = snapshot.val()
         that.site()
        })
      firebase.database().ref('/activeSite/').on('value', function(snapshot) {
         that.activeSite = snapshot.val()
         that.hour()
         that.site()
        })
      firebase.database().ref('/active/').on('value', function(snapshot) {
        that.active = snapshot.val()
        that.hour()
        that.site()
        })
      firebase.database().ref('/date_detect/').on('value', function(snapshot) {
        that.dated = snapshot.val()
        that.site()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/Detection').on('value', function(snapshot) {
        that.Detection = snapshot.val()
        console.log(that.Detection);
        })
      firebase.database().ref('/login/').on('value', function(snapshot) {
        that.login = snapshot.val()
        that.site()
        })
      firebase.database().ref('/member/').on('value', function(snapshot) {
        that.item = snapshot.val()
        that.site()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/date_maintenance').on('value', function(snapshot) {
        that.data_detail = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/status').on('value', function(snapshot) {
        that.status1 = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/September').on('value', function(snapshot) {
        that.sep = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/October').on('value', function(snapshot) {
        that.oct = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/November').on('value', function(snapshot) {
        that.nov = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/December').on('value', function(snapshot) {
        that.dec = snapshot.val()
        })
      firebase.database().ref('/Site/'+that.activeSite+'/January').on('value', function(snapshot) {
        that.jan = snapshot.val()
        })

    },
    hour () {
      this.activityChart.data.series = []
       this.activityChart.data.labels = []
      var data = []
      var data1 = []
      var data2 = []
      var data3 = []
      var data_Temperature_h = []
      var dataa_Temperature_h = []
      var time = []
      var activeSite1 = this.activeSite
      var a = 0
      var b = 0
      var c = 0
      var d = 0
        for (var variable1 in this.Site[activeSite1].moisture_h) {
          var n = 40000 - this.Site[activeSite1].moisture_h[variable1]
          var num = (n/40000) * 100
          data.push(num)
        }
        c = data.length - 12
        d = data.length - c
        for (var variable1 in this.Site[activeSite1].Temperature_h) {
          var temp = this.Site[activeSite1].Temperature_h[variable1].Temperature
          // temp = temp.toFixed(2)
          data_Temperature_h.push(temp)
          time.push(this.Site[activeSite1].Temperature_h[variable1].timee)
          // this.activityChart.data.labels.push(this.Site[activeSite1].Temperature_h[variable1])
        }
        for (var variable1 in this.Site[activeSite1].Temperature_h) {
          var Humid = this.Site[activeSite1].Temperature_h[variable1].Humidity
          // temp = temp.toFixed(2)
          dataa_Temperature_h.push(Humid)
          time.push(this.Site[activeSite1].Temperature_h[variable1].timee)
          // this.activityChart.data.labels.push(this.Site[activeSite1].Temperature_h[variable1])
        }
        console.log(data.length);
        for (var i = c; i < data.length; i++) {
          var temp = 0 + data_Temperature_h[i]
          var Humid = 0 + dataa_Temperature_h[i]
          this.activityChart.data.labels.push(time[i])
          data1.push(data[i].toFixed(2))
          data2.push(temp.toFixed(2))
          data3.push(Humid.toFixed(2))
        }

        this.tem = data2
        this.mo = data1
        this.hu = data3
      this.activityChart.data.series.push(data1,data2,data3)
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
    s_d () {
      if (this.detail === 't') {
        this.detail = 'f'
      }
      else   this.detail = 't'
    },
    Cancle () {
      this.sw = 'true'
    },
    save (num_day1,Last_maintenance) {
      num_day1 += 1
      firebase.database().ref('Site').child(this.activeSite).update({
        Last_maintenance: this.Last_maintenance,
        num_day: num_day1
      })
      firebase.database().ref('Site/'+ this.activeSite+'/date_maintenance').push({
        day: this.Last_maintenance
      })
      firebase.database().ref('Site').child(this.activeSite).update({
        first_maintenance: Last_maintenance
      })
      if ( Last_maintenance.substring(5,6) > this.Last_maintenance.substring(5,6)) {
        var day = +Last_maintenance.substring(8) + +this.Last_maintenance.substring(8)
      }
      else if ( Last_maintenance.substring(5,6) == this.Last_maintenance.substring(5,6)) {
        if ( Last_maintenance.substring(8) > this.Last_maintenance.substring(8)) {
            var day = (30 - Last_maintenance.substring(8)) + +this.Last_maintenance.substring(8)
        }
        else if (Last_maintenance.substring(8) == this.Last_maintenance.substring(8)) {
          var day = 30
        }
        else {
          var day = +this.Last_maintenance.substring(8) - +Last_maintenance.substring(8)
        }
      }
      firebase.database().ref('Site').child(this.activeSite).update({
        day_moisture : day
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
