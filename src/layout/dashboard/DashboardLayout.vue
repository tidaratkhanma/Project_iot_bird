<template>
  <div class="wrapper">

    <side-bar>
      <template slot="links"  v-if = "login === 'user'">
        <sidebar-link to="/dashboard" name="Dashboard" icon="ti-dashboard"/>
          <sidebar-link v-for="(s,key) in Site" @click.native ="tes" :to="'/ATM/' + key" icon="ti-location-pin" :name="s.name_site"/>
        <!-- <sidebar-link to="/sirinton" name="sirinton" icon="ti-location-pin"/>
        <sidebar-link to="/Larnplam" name="Larnplam" icon="ti-location-pin"/>
        <sidebar-link to="/car" name="Under the roof" icon="ti-location-pin"/> -->
        <sidebar-link to="/Report" name="Report" icon="ti-comment"/>
      </template>

      <template slot="links" v-else >
        <sidebar-link to="/dashboard" name="Dashboard" icon="ti-dashboard"/>
        <sidebar-link v-for="(s,key) in Site" @click.native ="tes" :to="'/ATM/' + key" icon="ti-location-pin" :name="s.name_site"/>
        <!-- <sidebar-link to="/ATM" name="ATM FITM" icon="ti-location-pin"/> -->
        <!-- <sidebar-link to="/sirinton" name="sirinton" icon="ti-location-pin"/>
        <sidebar-link to="/Larnplam" name="Larnplam" icon="ti-location-pin"/>
        <sidebar-link to="/car" name="Under the roof" icon="ti-location-pin"/> -->
        <!-- <sidebar-link to="/Report" name="Report" icon="ti-comment"/> -->
        <sidebar-link to="/Customer" name="Customer site" icon="ti-map-alt"/>
        <!-- <sidebar-link to="/Statistics" name="Statistics" icon="ti-pulse"/> -->
        <sidebar-link to="/show_report" :name="report" icon="ti-clipboard"/>
        <sidebar-link to="/setting" name="setting account" icon="ti-settings"/>
        <sidebar-link to="/setting_site" name="setting site" icon="ti-settings"/>
      </template>
    </side-bar>
    <div class="main-panel">
      <top-navbar></top-navbar>
      <dashboard-content @click.native="toggleSidebar">
      </dashboard-content>

      <content-footer></content-footer>
    </div>
  </div>
</template>
<style lang="scss">
</style>
<script>
import TopNavbar from "./TopNavbar.vue";
import ContentFooter from "./ContentFooter.vue";
import DashboardContent from "./Content.vue";
import MobileMenu from "./MobileMenu";
import firebase from 'firebase'
export default {
  data () {
    return {
      login: '',
      report: 0,
      Site: ''
    }
  },
  components: {
    TopNavbar,
    ContentFooter,
    DashboardContent,
    MobileMenu
  },
  created: function () {
    this.pullData()
  },
  methods: {
    pullData () {
      let that = this
      firebase.database().ref('/login/').on('value', function(snapshot) {
        that.login = snapshot.val()
      })
      firebase.database().ref('/Site/').on('value', function(snapshot) {
        that.Site = snapshot.val()
      })
      firebase.database().ref('/report/').on('value', function(snapshot) {
        that.report = snapshot.val()
        var count = 0
        for (var variable in that.report) {
          if (that.report[variable].status === 'false') {
            count = count + 1
          }
        }
        that.report = 'show report [ ' +count+' ]'

      })
    },
    toggleSidebar() {
      if (this.$sidebar.showSidebar) {
        this.$sidebar.displaySidebar(false);
      }
    },
    tes () {
    firebase.database().ref('activeSite').set(this.$route.params.id)
    }
  }
};
</script>
