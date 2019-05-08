<template>
  <div>
    <apexchart type=line height=500 :options="chartOptions" :series="series" />
  </div>
</template>

<script>
import Vue from 'vue'
import VueApexCharts from 'vue-apexcharts'
Vue.use(VueApexCharts)
Vue.component('apexchart', VueApexCharts)

export default {
  data: function() {
    return {
      series: [
        {
          name: "Jawa Barat",
          data: [44663441, 47330580, 49954727, 58362335, 63156760]
        },
        {
          name: "Kota Bandung",
          data: [5257439, 5564724, 5807564, 6061094, 5000625]
        }
      ],
      chartOptions: {
        chart: {
          shadow: {
            enabled: true,
            color: '#000',
            top: 18,
            left: 7,
            blur: 10,
            opacity: 1
          },
          toolbar: {
            show: false
          }
        },
        colors: ['#77B6EA', '#545454'],
        dataLabels: {
          enabled: true,
        },
        stroke: {
          curve: 'smooth'
        },
        title: {
          text: 'Perbandingan Jumlah Wisatawan',
          align: 'left'
        },
        grid: {
          borderColor: '#e7e7e7',
          row: {
            colors: ['#f3f3f3', 'transparent'], // takes an array which will be repeated on columns
            opacity: 0.5
          },
        },
        markers: {
          size: 6
        },
        xaxis: {
          categories: [2012, 2013, 2014, 2015, 2016],
          title: {
            text: 'Bulan'
          }
        },
        yaxis: {
          title: {
            text: 'Jumlah Wisatawan'
          },
          min: 0,
          max: 65000000,
          forceNiceScale: true
        },
        legend: {
          position: 'top',
          horizontalAlign: 'right',
          floating: true,
          offsetY: -25,
          offsetX: -5
        }
      }
    }
  },
}
</script>