<template>
  <div id="map"></div>
</template>
<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import "leaflet/dist/images/marker-shadow.png";
import "leaflet/dist/images/marker-icon.png";

export default {
  name: "MapaComponent",
  data: () => ({
    map: undefined,
  }),
  mounted() {
    this.setupMap();
  },
  methods: {
    setupMap() {
      this.map = L.map("map").setView([0, 0], 1);
      L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 19,
        attribution: "© OpenStreetMap",
      }).addTo(this.map);
      const leafletIcon = L.icon({
        iconUrl: "https://cdn-icons-png.flaticon.com/512/856/856332.png",
        iconSize: [45, 60],
        iconAnchor: [22, 94],
        popupAnchor:[12,-90]
      });
      const marker = L.marker([-3.042602743486333, -59.95165651808512], {
        icon: leafletIcon,
      }).addTo(this.map);
      const circle = L.circle([-3.0781166984188983, -60.00676763513346], {
        color: "red",
        fillColor: "#f03",
        fillOpacity: 0.5,
        radius: 500,
      }).addTo(this.map);
      const polygon = L.polygon([
        [-3.0984765828762013, -59.97596611648162],
        [-3.081323973313841, -59.9515710625983],
        [-3.1017196921402, -59.95683981683938],
      ]).addTo(this.map);
      marker.bindPopup("Eu sou um marcador").openPopup();
      circle.bindPopup("Eu sou um círculo");
      polygon.bindPopup("Eu sou um poligono");
    },
  },
};
</script>
<style scoped>
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
}
</style>
