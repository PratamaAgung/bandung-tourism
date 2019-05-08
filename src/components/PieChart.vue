<template>
  <div>
    <apexchart type=donut height=300px :series="series" :options="chartOptions" />
  </div>
</template>

<script>
import Vue from 'vue'
import VueApexCharts from 'vue-apexcharts'
Vue.use(VueApexCharts)
Vue.component('apexchart', VueApexCharts)

export default {
  name: "PieChart",
  data: function() {
    return {
      series: [],
      chartOptions: {
        labels: ['Wisata Alam', 'Wisata Budaya', 'Sejarah', 'Taman', 'Hiburan', 'Perbelanjaan'],
        responsive: [{
          breakpoint: 500,
          options: {
            legend: {
              position: 'bottom'
            }
          }
        }]
      },
      allBandungSeries: [7, 6, 10, 12, 9, 9],
      swkData: [
        {
          id: 0,
          name: "Cibeunying",
          series: [6, 3, 7, 11, 4, 4]
        },
        {
          id: 1,
          name: "Bojonagara",
          series: [0, 2, 1, 0, 2, 2]
        },
        {
          id: 2,
          name: "Tegallega",
          series: [0, 0, 1, 1, 0, 1]
        },
        {
          id: 3,
          name: "Karees",
          series: [1, 1, 1, 0, 2, 2]
        },
        {
          id: 4,
          name: "Ujung Berung",
          series: [0, 0, 0, 0, 1, 0]
        },
        {
          id: 5,
          name: "Gedebage",
          series: [0, 0, 0, 0, 0, 0]
        }
      ]
    }
  },
  methods: {
    getTotalDestination: function(series) {
      var totalDestination = 0
      series.forEach(dest => {
        totalDestination += dest
      })
      return totalDestination
    },
    updateSeries: function (swkId) {
      this.swkData.forEach(swk => {
        if (swk.id == swkId) {
          this.series = swk.series
        }
        var totalDestination = this.getTotalDestination(this.series)
        this.$emit("totalDestinationChanged", totalDestination)
      });
    },
    resetSeries: function () {
      this.series = this.allBandungSeries
      var totalDestination = this.getTotalDestination(this.series)
      this.$emit("totalDestinationChanged", totalDestination)
    }
  },
  mounted() {
    this.resetSeries()
    this.$root.$on('swkClickedIn', (swkId) => {
        this.updateSeries(swkId)
    })
    this.$root.$on('swkClickedOut', () => {
        this.resetSeries()
    })
  }
}
</script>