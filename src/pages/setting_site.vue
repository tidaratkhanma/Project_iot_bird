<template lang="html">
  <div class="">
    <div class="columns">
      <div class="column">
        <div class="field">
          <div class="control">
            <input class="input is-primary" v-model="data.name_site" type="text" placeholder="NAME SITE">
          </div>
        </div>
      </div>
      <div class="column">
        <div class="field">
          <div class="control"> Customer
            <div class="select is-primary" placeholder="Status">
              <select  v-model="data.cus" >
                <option selected v-for="(cus,key) in customer">{{cus.name_customer}}</option>
              </select>
            </div>
          </div>
        </div>
      </div>
      <div class="column is-one-fifth">
        <a class="button is-info is-outlined" @click="add()">Add</a>
      </div>
</div>
<article class="message ">
<b-container fluid>
  <!-- User Interface controls -->
  <b-row>
    <b-col md="6" class="my-1">
      <b-form-group horizontal label="Search" class="mb-0">
        <b-input-group>
          <b-form-input v-model="filter" placeholder="Type to Search" />
          <b-input-group-append>
            <b-btn :disabled="!filter" @click="filter = ''">Clear</b-btn>
          </b-input-group-append>
        </b-input-group>
      </b-form-group>
    </b-col>
  </b-row>

  <!-- Main table element -->
  <b-table show-empty
           stacked="md"
           :items="items"
           :fields="fields"
           :current-page="currentPage"
           :filter="filter"
           :sort-by.sync="sortBy"
           :sort-desc.sync="sortDesc"
           :sort-direction="sortDirection"
  >
    <template slot="Site" slot-scope="row"> {{row.value.Site}} </template>
    <template slot="Temperature" slot-scope="row">{{row.value.Temperature}}</template>
    <template slot="Humidity" slot-scope="row">{{row.value.Humidity}}</template>
    <template slot="Battery" slot-scope="row">{{row.value.Battery}}</template>
    <template slot="Status" slot-scope="row">{{row.value.Status}}</template>
    <template slot="action" slot-scope="row">
        <center>
      <!-- We use @click.stop here to prevent a 'row-clicked' event from also happening -->
        <b-button size="sm"class="mr-1" variant="warning" @click.stop="update(row.value.key, row.value.Site)">
          <i class="fa fa-edit"></i>
        </b-button>
      <b-button size="sm" variant="danger" @click.stop="deleted(row.value.key,row.value.cus)">
        <i class="fa fa-trash"></i></b-button>
    </center>
    </template>

  </b-table>
</b-container>
</article>

  </div>
</template>

<script>
import firebase from 'firebase'
import swal from 'sweetalert2'
const items = [
  { id: { id: '0001'}, name: { name: 'FITM SIDE'}, num: { num: 2}, status: { status: 'ปกติ'} },
  { id: { id: '0002'}, name: { name: 'ตึกศิรินทร'}, num: { num: 6}, status: { status: 'ปกติ'} },
  { id: { id: '0003'}, name: { name: 'อบต.เนินหอม'}, num: { num: 2}, status: { status: 'ปกติ'} },
]
export default {
  data () {
    return {
      items: [],
      fields: [
        { key: 'Site', label: 'Site', sortable: true, sortDirection: 'desc' },
        { key: 'Temperature', label: 'Temperature', sortable: true, 'class': 'text-center' },
        { key: 'Humidity', label: 'Humidity', sortable: true, 'class': 'text-center'},
        { key: 'Battery', label: 'Battery', sortable: true, 'class': 'text-center'},
        { key: 'Status', label: 'Status', sortable: true, 'class': 'text-center'},
        { key: 'action', label: 'Action', 'class': 'text-center'}
      ],
      currentPage: 1,
      perPage: 5,
      totalRows: items.length,
      pageOptions: [ 5, 10, 15 ],
      sortBy: null,
      sortDesc: false,
      sortDirection: 'asc',
      filter: null,
      modalInfo: { title: '', content: '' },
      show_member: '',
      data: {
        name_site: '',
        Last_maintenance: '',
        GunCheck: 1,
        Gunsound1: '1',
        Gunsound2: '1',
        Gunsound3: '1',
        Gunsound4: '1',
        Humidity: Math.floor(Math.random() * (100 - 1 + 1)) + 1,
        Sportlight1: '1',
        Sportlight2: '1',
        Sportlight3: '1',
        Sportlight4: '1',
        Temperature: Math.floor(Math.random() * (100 - 1 + 1)) + 1 ,
        moisture: Math.floor(Math.random() * (20000 - 1 + 1)) + 1 ,
        Battery: Math.floor(Math.random() * (16 - 1 + 1)) + 1 ,
        cus: ''
      },
      customer: ''
    }
  },
  computed: {
    sortOptions () {
      // Create an options list from our fields
      return this.fields
        .filter(f => f.sortable)
        .map(f => { return { text: f.label, value: f.key } })
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      var data = [], member = [], value = ''
      firebase.database().ref('/customer/').once('value').then(function (snapshot) {
        that.customer = snapshot.val()
      })
      firebase.database().ref('/Site/').once('value').then(function (snapshot) {
        that.show_member = snapshot.val()
        var status
        for (var variable in that.show_member) {
          if (that.show_member[variable].moisture<7700) {
            status = 'ปกติ'
          } else if (that.show_member[variable].moisture<15300) {
            status = 'น้ำยาใกล้หมด'
          } else if (that.show_member[variable].moisture>15300) {
            status = 'น้ำยาหมด'
          }
          value = {
            'Site': {
              'Site': that.show_member[variable].name_site
            },
            'Temperature': {
              'Temperature': that.show_member[variable].Temperature
            },
            'Humidity': {
              'Humidity': that.show_member[variable].Humidity
            },
            'Battery': {
              'Battery': that.show_member[variable].Battery
            },
            'Status': {
              'Status': status
            },
            'action': {
              'key': variable,
              'cus': that.show_member[variable].cus
            }
          }
          member.push(value)
        }
        that.items = member
      })

    },
    add () {
      var data_cus
      for (var variable in this.customer) {
        if (this.data.cus === this.customer[variable].name_customer) {
          data_cus = this.customer[variable].nnumber_customer + 1
          firebase.database().ref('customer').child(variable).update({
            nnumber_customer: data_cus
          })
        }
      }
      firebase.database().ref('Site').push(this.data)
      this.data.name_site = ''
      this.data.cus = ''

      this.pullData()
    },
    deleted (key,cus) {
      swal({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
      }).then((result) => {
        if (result.value) {
          firebase.database().ref('Site').child(key).remove()
          var data_cus
          for (var variable in this.customer) {
            if (cus === this.customer[variable].name_customer) {
              data_cus = this.customer[variable].nnumber_customer - 1
              firebase.database().ref('customer').child(variable).update({
                nnumber_customer: data_cus
              })
            }
          }
          swal(
            'Deleted!',
            'Your file has been deleted.',
            'success'
          )
          this.pullData()
        }
      })
    },
    update (key) {
      swal({
        title: 'Edit Site',
        input: 'text',
        inputPlaceholder: 'Name Site',
        showCancelButton: true,
        inputValidator: (value) => {
          return new Promise((resolve) => {
            if (value !== '') {
              firebase.database().ref('Site').child(key).update({
                name_site: value
              })
              swal('Successfully, Name Site changed to ' + value)
              this.pullData()
            } else {
              resolve('You need to edit Name Site')
            }
          })
        }
      })
      this.pullData()
    }
  }
}
</script>

<style lang="css">
</style>
