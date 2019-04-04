<template>
  <div>

    <article class="message is-warning">
  <div class="message-body">
      <div class="field">
        <label class="label">Username</label>
        <div class="control has-icons-left has-icons-right">
          <input class="input  is-success" type="text" :value="active" name="username" readonly>
          <span class="icon is-small is-left">
            <i class="fas fa-user"></i>
          </span>
        </div>
      </div>

      <div class="field">
        <label class="label">Telephone</label>
        <div class="control has-icons-left has-icons-right">
          <input class="input is-success" type="number" size="10" v-model="data.tel" placeholder="Telephone">
          <span class="icon is-small is-left">
            <i class="fas fa-phone-volume"></i>
          </span>
        </div>
      </div>

      <div class="field">
        <label class="label">Message</label>
        <div class="control">
          <textarea class="textarea" placeholder="Textarea" v-model="data.message"></textarea>
        </div>
      </div>
      <div class="field is-grouped">
        <div class="control">
          <button class="button is-link" @click="add()">Submit</button>
        </div>
        <div class="control">
          <button class="button is-text">Cancel</button>
        </div>
      </div>

  </div>
</article>
  </div>
</template>
<script>
import firebase from 'firebase'
import swal from 'sweetalert2'
export default {
  data() {
    return {
      data: {
        username: '',
        tel: '',
        message: '',
        status: ''
      },
      active: ''
    }
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      firebase.database().ref('/active/').on('value', function(snapshot) {
        that.active = snapshot.val()
      })
    },
    add () {
      swal({
        title: 'Are you sure?',
        text: "You want to send a message.",
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes it\'s'
      }).then((result) => {
        this.data.username = this.active
        this.data.status = 'false'
        firebase.database().ref('report').push(this.data)
        this.data = ''
        if (result.value) {
          swal(
            'Success!',
            'success'
          )
        }
      })
    },
  }
}
</script>
<style>
</style>
