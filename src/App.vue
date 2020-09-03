<template>
  <v-app>
    <v-app-bar
        app
        color="primary"
        dark
    >
      <h4>Dashboard</h4>
      <v-spacer></v-spacer>
      <div>{{ $vuetify.breakpoint.name }}</div>
    </v-app-bar>

    <v-content>
      <dashboard :dashboardConfig="dashboardJson"/>
    </v-content>
  </v-app>
</template>

<script>
import Dashboard from './components/lib/Dashboard';
import DASHBOARD_JSON from './assets/mock-data/dashboard.json';

export default {
  name: 'App',
  components: {
    'dashboard': Dashboard,
  },

  data: () => ({
    dashboardJson: DASHBOARD_JSON
  }),
}

</script>
