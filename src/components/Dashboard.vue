<template>
  <v-container fluid>
    <v-row align="center">

      <v-col class="d-flex" cols="2">
        <v-select :items="locations" :value="location" label="Countries" outlined @change="fetchLocationData"></v-select>
      </v-col>

      <v-col cols="12">
        <v-card>
          <v-toolbar color="light-green" dark>
            <v-toolbar-title>COVID 19 Total Cumulative Cases - {{location}}</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <line-chart :chart-data="chartdata"></line-chart>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import LineChart from './LineChart.js'
import axios from 'axios'

export default {
  components: { LineChart },
  data: function () {
    return {
      chartdata: {
        labels: [],
        datasets: [],
        chartColors: {
          red: 'rgb(255, 99, 132)',
          orange: 'rgb(255, 159, 64)',
          yellow: 'rgb(255, 205, 86)',
          green: 'rgb(75, 192, 192)',
          blue: 'rgb(54, 162, 235)',
          purple: 'rgb(153, 102, 255)',
          grey: 'rgb(201, 203, 207)'
        },
        locations: [],
        location: 'Nepal'
      }
    }
  },
  methods: {
    fetchLocationData (location) {
      axios.get(`/data/${location}`).then(data => {
        this.location = location
        this.chartdata = {
          labels: data.data.map(x => x[0]),
          datasets: [
            {
              label: location,
              fill: false,
              borderColor: 'rgb(54, 162, 235)',
              data: data.data.map(x => x[1])
            }
          ]
        }
      })
    }
  },
  mounted () {
    axios
      .get('/locations')
      .then(data => {
        this.locations = data.data.map(x => x[0])
      })
      .then(this.fetchLocationData('Nepal'))
  }
}
</script>
