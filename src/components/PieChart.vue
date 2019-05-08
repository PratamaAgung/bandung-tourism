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
      series: [7, 6, 10, 12, 9, 9],
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
      }
    }
  },
  methods: {
    reset: function () {
          this.series = [10, 6, 10, 12, 9, 9]
        },
  },
  mounted() {
    this.$root.$on('swkClickedIn', (e) => {
          this.reset();
          console.log(e)
      })
  }
}
</script>