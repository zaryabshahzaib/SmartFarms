<template>
  <section class="notifications navbar-notifications">
    <header class="header">
      <h6 class="my-3 text-center">You have 2 notifications</h6>
    </header>
    <NewNotifictionsList v-if="newNotifications" />
    <NotifictionsList v-else-if="notificationsTabSelected === 1" />
    <Messages v-else-if="notificationsTabSelected === 2" />
    <Progress v-else-if="notificationsTabSelected === 3" />
    <NotifictionsList v-else/>
    <footer class="text-sm footer px-4 py-2">
      <span class="fs-mini">Synced at: 1 Feb 2020 16:47</span>
      <b-button
        variant="link"
        @click="loadNotifications"
        :class="{disabled: isLoad, 'btn-xs float-right py-0': true}"
      >
        <span v-if="isLoad"><i class="la la-refresh la-spin" /> Loading...</span>
        <i v-else class="la la-refresh" />
      </b-button>
      
    </footer>
  </section>
  
</template>

<script>
import Vue from 'vue';

import NotifictionsList from './NotificationsDemo/NotificationsList';
import NewNotifictionsList from './NotificationsDemo/NewNotificationsList';
import Messages from './NotificationsDemo/Messages';
import Progress from './NotificationsDemo/Progress';
import Highcharts from 'highcharts';
import exporting from 'highcharts/modules/exporting';
import exportData from 'highcharts/modules/export-data';
import {chartData, liveChart, liveChartInterval} from './mock';


exporting(Highcharts);
exportData(Highcharts);

import { Chart } from 'highcharts-vue';

export default {
  name: 'Notification',
  components: {
    NotifictionsList, NewNotifictionsList, Messages, Progress,highcharts: Chart
  },
  data() {
    return {
      cd: chartData,
      ld: liveChart,
      initEchartsOptions: {
        renderer: 'canvas'
      },
      notificationsTabSelected: 1,
      newNotifications: null,
      isLoad: false,
    };
  },
  methods: {
    loadNotifications() {
      Vue.set(this, 'isLoad', true);

      setTimeout(() => {
        Vue.set(this, 'newNotifications', 'new notifications component');
        Vue.set(this, 'isLoad', false);
      }, 1500);
    },
  },
};
</script>

<style src="./Notifications.scss" lang="scss" />
