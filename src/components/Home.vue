<template>
  <div class="map ">
      <h1>Desk Relawan</h1>
      <div style="height: 500px; width: 100%">
        <l-map :zoom="zoom" :center="center">
          <l-marker :lat-lng="center"></l-marker>
          <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
        </l-map>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'© <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 12,
      center: [-8.101452, 112.160277],
      bounds: null,
    };
  }
}
</script>
