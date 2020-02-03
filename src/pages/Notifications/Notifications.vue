<template>
  <div>
    <!-- <b-breadcrumb>
      <b-breadcrumb-item>YOU ARE HERE</b-breadcrumb-item>
      <b-breadcrumb-item active>UI Notifications</b-breadcrumb-item>
    </b-breadcrumb> -->
    <!-- <h1 class="page-title">Messages - <span class="fw-semi-bold">Notifications</span>
    </h1> -->
    <Widget
         title="<h5 style = 'text-align:center;'> <span style = 'font-size:27px;' class='fw-bold'>Recommendations</span></h5>"
         customHeader settings close
    >
     <b-row>
        <!-- <b-col lg = "1">
        </b-col> -->
     <b-col >
      
      <table class="table table-striped" >
           <thead>
             <tr>
               <th>Urgency</th>
               <th>Type</th>
               <th>Message</th>
               <th>Recommendation</th>
             </tr>
           </thead>
           <tbody>
             <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "danger"></b-icon></p></td>
               <td style = 'font-size:18px;'>Diseased Crop</td>
               <td style = 'font-size:18px;'>Mold detected on the leaves of tomato crop</td>
               <td style = 'font-size:18px;'>Spray the field evenly with 5 litres of pesticide</td>
             </tr>
             <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "danger"></b-icon></p></td>
               <td style = 'font-size:18px;'>Moisture </td>
               <td style = 'font-size:18px;'>Moisture levels are higher than specified limit</td>
               <td style = 'font-size:18px;'>Field should not be watered for the next 23 hours</td>
             </tr>
             <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "warning"></b-icon></p></td>
               <td style = 'font-size:18px;'>Nutrients</td>
               <td style = 'font-size:18px;'>Potassium levels are below the required limit!</td>
               <td style = 'font-size:18px;'>Add 10 kg of Potassium Fertilizer!</td>
             </tr>
              <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "warning"></b-icon></p></td>
               <td style = 'font-size:18px;'>pH</td>
               <td style = 'font-size:18px;'>pH level is slightly alkaline (9.3)</td>
               <td style = 'font-size:18px;'>Sprinkle 2 litres of nitric acid evenly across the field</td>
             </tr>
              <tr>
               <td><p class = "h3" ><b-icon icon="alert-octagon-fill" variant = "warning"></b-icon></p></td>
               <td style = 'font-size:18px;'>Weather</td>
               <td style = 'font-size:18px;'>Light showers expected tomorrow</td>
               <td style = 'font-size:18px;'>Do not water the field for the next 12 hours</td>
             </tr>
             </tr>
             </tr>
           </tbody>
         </table>
          </b-col>
           </b-row>
        </Widget>
   
    <Widget
      close collapse settings customHeader
    >
    <highcharts :options="cd.highcharts.mixed"></highcharts>
    </Widget>
  </div>

  



</template>

<script>
import Widget from '@/components/Widget/Widget';
import Vue from 'vue';

import Highcharts from 'highcharts';
import exporting from 'highcharts/modules/exporting';
import exportData from 'highcharts/modules/export-data';
import {chartData, liveChart, liveChartInterval} from './mock';


exporting(Highcharts);
exportData(Highcharts);

import { Chart } from 'highcharts-vue';

export default {
  name: 'Notifications',
  data() {
    return {
      cd: chartData,
      ld: liveChart,
      initEchartsOptions: {
        renderer: 'canvas'
      },
    }
  },
  components: { Widget, highcharts: Chart },
  methods: {
    addSuccessNotification() {
      this.$toasted.success('Showing success message was successful!', {
        action: {
          text: 'Close',
          onClick: (e, toastObject) => {
            toastObject.goAway(0);
          }
        }
      })
    },
    addInfoNotification() {
      this.$toasted.info('Launching thermonuclear war...', {
        action: {
          text: 'Cancel launch',
          onClick: (e, toastObject) => {
            toastObject.text('Thermonuclear war averted').goAway(1000);
          }
        }
      });
    },
    addErrorNotification() {
      this.$toasted.error('Launching thermonuclear war...', {
        action: [
          {
            text: 'Cancel',
            onClick: (e, toastObject) => {
              toastObject.el.classList.remove('info');
              toastObject.el.classList.add('success');
              toastObject.text('Alien planet destroyed!').goAway(2000);
            }
          }
        ]
      });
    },
    toggleLocation(position = 'top-right') {
      this.$toasted.options.position = position;
      this.$toasted.show(null);
    },
  },
  created() {
    // this.$toasted.show('Thanks for checking out Messenger!');
  },
};
</script>

<style src="./Notifications.scss" lang="scss" scoped />
