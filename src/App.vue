<template>
  <div id="app">
    <Map @click="onClick($event)"/>
    <Graph/>
  </div>
</template>

<script>
import Map from './components/Map.vue'
import Graph from './components/Graph.vue'

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
