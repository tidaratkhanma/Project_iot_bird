<template>
  <div>

    <!--Charts-->
    <div class="row">
      <div class="col-12">
        <article class="message is-dark">
          <div class="message-body">
            <div class="columns">
          <div class="column">
            จำนวนนกที่พบ
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="17" placeholder="17">
          </div>
          </div>
          </div>
          <div class="column">
            อุณหภูมิ
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="27C" placeholder="27C">
          </div>
          </div>
          </div>
          <div class="column">
            ความชื้น
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="74%" placeholder="74%">
          </div>
          </div>
          </div>
        </div>
              </div>
        </article>
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
      <div class="col-12">
        <article class="message is-dark">
          <div class="message-body">
            สถิติการเติมยา</br>
            เติมน้ำยาครั้งล่าสุด 10 ก.ย. 2561 </br> </br>
            <div class="columns">
          <div class="column">
            เครื่องไล่นก 1
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="2">
          </div>
        </div>
          </div>
          <div class="column">
            เครื่องไล่นก 2
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="5">
          </div>
        </div>
          </div>
          <div class="column">
            เครื่องไล่นก 3
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="8">
          </div>
        </div>
          </div>
          <div class="column">
            เครื่องไล่นก 4
            <div class="field">
          <div class="control">
            <input class="input is-success"  type="text" value ="2">
          </div>
        </div>
          </div>
        </div>
              </div>
        </article>
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
      </div>
    </div>

  </div>
</template>
<script>
import { StatsCard, ChartCard } from "@/components/index";
import Chartist from 'chartist';
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
          type: "warning",
          icon: "ti-server",
          title: "Capacity",
          value: "105GB",
          footerText: "Updated now",
          footerIcon: "ti-reload"
        },
        {
          type: "success",
          icon: "ti-wallet",
          title: "Revenue",
          value: "$1,345",
          footerText: "Last day",
          footerIcon: "ti-calendar"
        },
        {
          type: "danger",
          icon: "ti-pulse",
          title: "Errors",
          value: "23",
          footerText: "In the last hour",
          footerIcon: "ti-timer"
        },
        {
          type: "info",
          icon: "ti-twitter-alt",
          title: "Followers",
          value: "+45",
          footerText: "Updated now",
          footerIcon: "ti-reload"
        }
      ],
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
      },
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
      preferencesChart: {
        data: {
          labels: ["62%", "32%", "6%"],
          series: [62, 32, 6]
        },
        options: {}
      }
    };
  }
};
</script>
<style>
</style>
