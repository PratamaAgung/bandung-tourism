<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">Bandung Tourism</b-navbar-brand>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <b-badge pill variant="light" id="swk-active" ref="swk-active">Kota Bandung</b-badge>
          </b-nav-form>
        </b-navbar-nav>
      </b-navbar>
    </div>
    <b-card bg-variant="light" text-variant="white" style="s">
      <Map/>
    </b-card>
    <div style="padding:10px">
      <b-card-group deck>
        <b-card bg-variant="primary" text-variant="white" header="Jumlah Objek Wisata" class="text-center">
          <b-card-text class="align-middle">
            <h1 class="display-1" id="total-destination" ref="total-destination">11</h1>
          </b-card-text>
        </b-card>

        <b-card bg-variant="light" text-variant="black" header="Jenis Objek Wisata" class="text-center">
          <PieChart @totalDestinationChanged="updateTotalDestination($event)"/>
        </b-card>

      </b-card-group>
    </div>
  </div>
</template>

<script>
import Map from './components/Map.vue'
import BootstrapVue from 'bootstrap-vue'
import Vue from 'vue'
import PieChart from './components/PieChart.vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue)

export default {
  name: 'app',
  data: function(){
    return {
      swk : ["Cibeunying", "Bojonagara", "Tegalega", "Karees", "Ujungberung", "Gedebage"]
    }
  },
  components: {
    Map,
    PieChart
  },
  methods: {
    updateTotalDestination: function(e) {
      this.$refs["total-destination"].innerText = e
    },
    setSwk: function(e) {
      this.$refs['swk-active'].innerText = this.swk[e]
    },
    setKotaBandung: function() {
      this.$refs['swk-active'].innerText = "Kota Bandung"
    }
  },
  mounted() {
    this.$root.$on('swkClickedIn', (swkId) => {
        this.setSwk(swkId)
    })
    this.$root.$on('swkClickedOut', () => {
        this.setKotaBandung()
    })
  }
}

</script>


<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
