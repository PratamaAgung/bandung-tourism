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
      layers: [
        {
          id: 0,
          name: "Bandung Map",
          active: true,
          features: [
            {
              id: 0,
              name: "Cibeunying",
              type: "polygon",
              coords: [
                [-6.843263, 107.597039],
                [-6.889269, 107.556148],
                [-6.963528, 107.626210],
                [-6.909502, 107.736855]
              ],
              center: [-6.911056, 107.636914]
            }
          ]
        }
      ],
    }
  },
  methods: {
    initMap() {
      this.map = L.map('map').setView([-6.911056, 107.636914], 13);
      this.map.dragging.disable()
      this.tileLayer = L.tileLayer(
        'https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png',
        {
          maxZoom: 20,
          minZoom: 10,
          bounds: [
                [-6.843263, 107.597039],
                [-6.889269, 107.556148],
                [-6.963528, 107.626210],
                [-6.909502, 107.736855]
              ],
          attributionControl: false
        }
      );
      this.tileLayer.addTo(this.map);
    },
    initLayers() {
      this.layers.forEach((layer) => {
        const markerFeatures = layer.features.filter(feature => feature.type === 'marker');
        const polygonFeatures = layer.features.filter(feature => feature.type === 'polygon');
        markerFeatures.forEach((feature) => {
          feature.leafletObject = L.marker(feature.coords)
            .bindPopup(feature.name);
        });
        polygonFeatures.forEach((feature) => {
          feature.leafletObject = L.polygon(feature.coords, {
            'label' : feature.name,
            'center' : feature.center
          })
          feature.leafletObject.bindPopup(feature.name)
          feature.leafletObject.on('mouseover', this.onPolyHover)
          feature.leafletObject.on('mouseout', this.onPolyOut)
          feature.leafletObject.on('click', this.onPolyClickIn)
        });
        layer.features.forEach((feature) => {
          if (layer.active) {
            feature.leafletObject.addTo(this.map)
          }
        })
      })
    },
    onPolyClickIn(event){
      this.map.fitBounds(event.target.getBounds())
      event.target.on('click', this.onPolyClickOut)
    },
    onPolyClickOut(event){
      event.target.setStyle({
        fillOpacity: 0.5
      })
      this.map.setView(event.target.options.center, 13)
      event.target.on('click', this.onPolyClickIn)
    },
    onPolyHover(event){
      event.target.openPopup();
    },
    onPolyOut(event){
      event.target.closePopup();
    }
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
