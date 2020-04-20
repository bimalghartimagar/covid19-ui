<template>
  <v-container fluid>
    <v-row align="center">
      <v-col class="d-flex" cols="4" md="5" sm="12" xs="12">
        <v-select
          :items="locations"
          :value="location"
          label="Countries"
          outlined
          @change="fetchLocationData"
        ></v-select>
      </v-col>

      <v-col cols="12">
        <v-card>
          <v-toolbar color="light-green" dark>
            <v-toolbar-title>COVID 19 Total Cumulative Cases - {{location}}</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <line-chart :chart-data="lineData"></line-chart>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col cols="12">
        <v-card>
          <v-toolbar color="light-green" dark>
            <v-toolbar-title>COVID 19 Daily New Cases - {{location}}</v-toolbar-title>
          </v-toolbar>
          <v-card-text>
            <bar-chart :chart-data="barData"></bar-chart>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios'
import LineChart from './LineChart.js'
import BarChart from './BarChart.js'

export default {
  components: { LineChart, BarChart },
  data: function () {
    return {
      lineData: {
        labels: [],
        datasets: []
      },
      barData: {
        labels: [],
        datasets: []
      },
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
  },
  methods: {
    fetchLocationData (location) {
      axios.get(`/data/${location}`).then(data => {
        this.location = location

        const lineDataOpts = [
          { id: 1, color: 'blue', label: 'Total Cases' }, // total cumulative
          { id: 3, color: 'red', label: 'Total Deaths' } // total deaths
        ]

        const barDataOpts = [
          { id: 2, color: 'orange', label: 'Daily New Cases' }, // daily new cases
          { id: 4, color: 'red', label: 'Daily Deaths' } // daily deaths
        ]

        this.lineData = this.getUpdatedChartData(data, lineDataOpts)

        this.barData = this.getUpdatedChartData(data, barDataOpts)
      })
    },
    getUpdatedChartData (data, opts) {
      const datasets = opts.map(element => {
        return {
          label: element.label,
          fill: false,
          borderColor: this.chartColors[element.color],
          backgroundColor: this.chartColors[element.color],
          data: data.data.map(x => x[element.id])
        }
      })
      return {
        labels: data.data.map(x => x[0]),
        datasets: datasets
      }
    }
  },
  mounted () {
    axios
      .get('/locations')
      .then(data => {
        this.locations = data.data.map(x => x[0])
      })
      .then(this.fetchLocationData(this.location))
  }
}
</script>
