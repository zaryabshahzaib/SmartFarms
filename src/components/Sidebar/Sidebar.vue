<template>
  <b-collapse class="sidebar-collapse" id="sidebar-collapse" :visible="sidebarOpened">
  <nav
    :class="{sidebar: true}"
  >
    <header class="logo">
      <router-link to="/app/dashboard">Smart <span class="fw-semi-bold">Farms</span></router-link>
    </header>
    <ul class="nav">
      <NavLink
              :activeItem="activeItem"
              header="Dashboard"
              link="/app/dashboard"
              iconName="flaticon-home"
              index="dashboard"
              isHeader
      />
      <NavLink
              header="Recommendations"
              link="/app/recommendations"
              iconName="flaticon-alarm"
              index="recommendations"
              isHeader
      />
      <NavLink
              header="DiseasePrediction"
              link="/app/diseaseprediction"
              iconName="flaticon-alarm"
              index="diseaseprediction"
              isHeader
      />
      <!-- <NavLink
              header="Analytics"
              link="/app/notifications"
              iconName="flaticon-radar"
              index="notifications"
              isHeader
      /> -->
      <!-- <NavLink
              :activeItem="activeItem"
              header="Environment"
              link="/app/components"
              iconName="flaticon-cloud"
              index="components"
              :childrenLinks="[
          { header: 'Light', link: '/app/components/charts' },
          { header: 'Temperature', link: '/app/components/icons' },
          { header: 'Humidity', link: '/app/components/maps' },
        ]"
      />
      <NavLink
              :activeItem="activeItem"
              header="Soil"
              link="/app/components"
              iconName="flaticon-tabs"
              index="components"
              :childrenLinks="[
          { header: 'Moisture', link: '/app/components/charts' },
          { header: 'Nutrients', link: '/app/components/icons' },
        ]"
      /> -->
    </ul>
    <h5 class="navTitle d-sm-down-none">
      Indicators
      <a class="actionLink">
        <i class="la la-plus float-right" />
      </a>
    </h5>
    <ul class="sidebarLabels d-sm-down-none">
      <li>
        <a href="#">
          <i class="fa fa-circle text-success mr-2" />
          <span class="labelName">Ok</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="fa fa-circle text-warning mr-2" />
          <span class="labelName">Warning</span>
        </a>
      </li>
      <li>
        <a href="#">
          <i class="fa fa-circle text-danger mr-2" />
          <span class="labelName">Urgent</span>
        </a>
      </li>
    </ul>
  </nav>
  </b-collapse>
</template>

<script>
import { mapState, mapActions } from 'vuex';
import NavLink from './NavLink/NavLink';

export default {
  name: 'Sidebar',
  components: { NavLink },
  data() {
    return {
      alerts: [
        {
          id: 0,
          title: 'Sales Report',
          value: 15,
          footer: 'Calculating x-axis bias... 65%',
          color: 'info',
        },
        {
          id: 1,
          title: 'Personal Responsibility',
          value: 20,
          footer: 'Provide required notes',
          color: 'danger',
        },
      ],
    };
  },
  methods: {
    ...mapActions('layout', ['changeSidebarActive', 'switchSidebar']),
    setActiveByRoute() {
      const paths = this.$route.fullPath.split('/');
      paths.pop();
      this.changeSidebarActive(paths.join('/'));
    },
  },
  created() {
    this.setActiveByRoute();
  },
  computed: {
    ...mapState('layout', {
      sidebarOpened: state => !state.sidebarClose,
      activeItem: state => state.sidebarActiveElement,
    }),
  },
};
</script>

<!-- Sidebar styles should be scoped -->
<style src="./Sidebar.scss" lang="scss" scoped/>
