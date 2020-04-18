<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        COVID 19 Dashboard
      </div>

      <v-spacer></v-spacer>

    </v-app-bar>

    <v-content>
      <Dashboard/>
    </v-content>
  </v-app>
</template>

<script>
import Dashboard from './components/Dashboard'

export default {
  name: 'App',

  components: {
    Dashboard
  },

  data: () => ({
    //
  })
}
</script>
