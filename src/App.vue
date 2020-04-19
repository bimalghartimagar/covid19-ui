<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">COVID 19 Dashboard</div>

      <v-spacer></v-spacer>

      <v-btn text @click="showAbout = true">About</v-btn>
      <v-menu :open-on-hover="true" :offset-y="true">
        <template v-slot:activator="{ on }">
          <v-btn icon dark href v-on="on">
            <v-img max-width="28" :src="require('./assets/github.png')" />
          </v-btn>
        </template>
        <v-list>
          <v-list-item target="_blank" href="https://github.com/bimalghartimagar/covid19-ui">
            <v-list-item-title>COVID19 - UI</v-list-item-title>
            <v-list-item-action>
              <v-btn icon>
                <v-icon color="blue">mdi-open-in-new</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
          <v-list-item target="_blank" href="https://github.com/bimalghartimagar/covid19-api">
            <v-list-item-title>COVID19 - API</v-list-item-title>
            <v-list-item-action>
              <v-btn icon>
                <v-icon color="blue">mdi-open-in-new</v-icon>
              </v-btn>
            </v-list-item-action>
          </v-list-item>
        </v-list>
      </v-menu>
    </v-app-bar>

    <v-content>
      <Dashboard />
    </v-content>
    <About :dialog="showAbout" v-on:close-about="closeDialog" />
  </v-app>
</template>

<script>
import Dashboard from './components/Dashboard'
import About from './components/About'

export default {
  name: 'App',

  components: {
    Dashboard,
    About
  },

  data: () => ({
    showAbout: false
  }),
  methods: {
    closeDialog () {
      this.showAbout = false
    }
  }
}
</script>
