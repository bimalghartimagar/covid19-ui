<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500">
      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>About Dashboard</v-card-title>
        <v-list dense flat>
          <v-subheader>Frontend</v-subheader>
          <v-list-item-group color="primary">
            <v-list-item v-for="(item, i) in frontend" :key="i" target="_blank" :href="item.link">
              <v-list-item-content>
                <v-list-item-title>
                  <v-btn small text>{{item.name}}</v-btn>
                </v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon>
                  <v-icon color="blue">mdi-open-in-new</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list-item-group>
          <v-divider></v-divider>
          <v-subheader>API</v-subheader>
          <v-list-item-group color="primary">
            <v-list-item v-for="(item, i) in api" :key="i" target="_blank" :href="item.link">
              <v-list-item-content>
                <v-list-item-title>
                  <v-btn small text>{{item.name}}</v-btn>
                </v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon>
                  <v-icon color="blue">mdi-open-in-new</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list-item-group>
          <v-divider></v-divider>
          <v-subheader>Data Source</v-subheader>
          <v-list-item-group color="primary">
            <v-list-item v-for="(item, i) in data" :key="i" target="_blank" :href="item.link">
              <v-list-item-content>
                <v-list-item-title>
                  <v-btn small text>{{item.name}}</v-btn>
                </v-list-item-title>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn icon>
                  <v-icon color="blue">mdi-open-in-new</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
          </v-list-item-group>
        </v-list>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" text @click="$emit('close-about')">Okay</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: ['dialog'],
  data () {
    return {
      frontend: [
        { name: 'Vue', link: 'https://vuejs.org/' },
        { name: 'Vuetify', link: 'https://vuetifyjs.com/' },
        { name: 'Chart.js', link: 'https://www.chartjs.org/' },
        { name: 'vue-chartjs', link: 'https://vue-chartjs.org/' }
      ],
      api: [
        { name: 'Flask', link: 'https://flask.palletsprojects.com/' },
        { name: 'pandas', link: 'https://pandas.pydata.org/' }
      ],
      data: [
        {
          name: 'Data on COVID-19',
          link: 'https://github.com/owid/covid-19-data'
        }
      ]
    }
  }
}
</script>
