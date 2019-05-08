<template>
  <div>
    <div>
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand href="#">Bandung Tourism</b-navbar-brand>
      </b-navbar>
    </div>
    <b-card bg-variant="light" text-variant="white" style="s">
      <Map/>
    </b-card>
    <div style="padding:10px">
      <b-card-group deck>
        <b-card bg-variant="primary" text-variant="white" header="Jumlah Objek Wisata" class="text-center">
          <b-card-text class="align-middle">
            <h1 class="display-1">11</h1>
          </b-card-text>
        </b-card>

        <b-card bg-variant="light" text-variant="black" header="Jenis Objek Wisata" class="text-center">
          <Graph/>
        </b-card>

      </b-card-group>
    </div>
  </div>
</template>

<script>
import Map from './components/Map.vue'
import Graph from './components/Graph.vue'
import BootstrapVue from 'bootstrap-vue'
import Vue from 'vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

Vue.use(BootstrapVue)

export default {
  name: 'app',
  components: {
    Map,
    Graph
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
