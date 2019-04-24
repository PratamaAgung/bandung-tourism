<template>
  <div class="map" id="map">
  </div>
</template>

<script>
import L from 'leaflet'
export default {
  name: 'Map',
  data() {
    return {
      map: null,
      tileLayer: null,
      layers: [],
    }
  },
  methods: {
    initMap() {
      this.map = L.map('map').setView([-6.911056, 107.636914], 13);
      this.tileLayer = L.tileLayer(
        'https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png',
        {
          maxZoom: 20
        }
      );
      this.tileLayer.addTo(this.map);
    },
    initLayers() {},
  },
  mounted() {
    this.initMap();
    this.initLayers();
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.map {
  height: 600px;
}
</style>
