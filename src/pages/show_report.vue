<template lang="html">
  <div class="">
    <article class="message is-warning" v-for = "(data,key) in report"  v-if = "data.status === 'false'">
      <div class="message-body">
    <b>  Name: </b>  {{data.username}} &nbsp;&nbsp;&nbsp;
        <b> telephone: </b>   {{data.tel}} </br>
          <b> message </b> </br>{{data.message}} </br>
      </div>
      <div class="columns">
        <div class="column is-two-thirds"></div>
        <div class="column">
        </div>
        <div class="column">
          <a class="button is-success" @click="Finished(key)" v-if = "data.status === 'false'">
          <span class="icon is-small">
            <i class="fas fa-check"></i>
          </span>
          <span>Finished editing</span>
        </a>
        </div>
    </div>
    </article>
    <article class="message is-warning" v-for = "(data,key) in report"  v-if = "data.status === 'true'">
      <div class="message-body">
    <b>  Name: </b>  {{data.username}} &nbsp;&nbsp;&nbsp;
        <b> telephone: </b>   {{data.tel}} </br>
          <b> message </b> </br>{{data.message}} </br>
      </div>
      <div class="columns">
        <div class="column is-two-thirds"></div>
        <div class="column">
        </div>
        <div class="column">
        <a class="button is-danger" @click="del(key)" v-if = "data.status === 'true'">
        <span class="icon is-small">
          <i class="fas fa-times"></i>
        </span>
        <span>Delete</span>
      </a>
        </div>
    </div>
    </article>
  </div>
</template>
<script>
import firebase from 'firebase'
import swal from 'sweetalert2'
export default {
  data () {
    return {
      report: ''
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      var data = [], member = [], value = ''
      firebase.database().ref('/report/').on('value', function(snapshot) {
        that.report = snapshot.val()
      })
    },
    del (key) {
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
          firebase.database().ref('report').child(key).remove()
          swal(
            'Deleted!',
            'Your file has been deleted.',
            'success'
          )
          this.pullData()
        }
      })
    },
    Finished (key) {
      swal({
        title: 'Are you sure?',
        text: "You have finished editing!",
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, finished it!'
      }).then((result) => {
        if (result.value) {
          firebase.database().ref('report').child(key).update({
            status: 'true'
          })
          this.pullData()
        }
      })
    }
  }
}
</script>

<style lang="css">
</style>
