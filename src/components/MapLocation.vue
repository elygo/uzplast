<template>
  <div id="map" style="height: 100%"></div>
</template>

<script>
import { ref, onMounted } from "vue";
import "ol/ol.css";
import Map from "ol/Map";
import TileLayer from "ol/layer/Tile";
import VectorLayer from "ol/layer/Vector";
import VectorSource from "ol/source/Vector";
import Icon from "ol/style/Icon";
import Feature from "ol/Feature";
import { Point } from "ol/geom";
import { Style, Circle, Fill } from "ol/style";
import OSM from "ol/source/OSM";
import { fromLonLat } from "ol/proj";
import View from "ol/View";

export default {
  name: "MapLocation",
  setup() {
    onMounted(() => {
      const iconFeature = new Feature({
        geometry: new Point(
          fromLonLat([65.34803, 40.101679], "EPSG:4326", "EPSG:3857")
        ),
        name: "Somewhere near Nottingham",
      });

      const map = new Map({
        target: "map",
        layers: [
          new TileLayer({
            source: new OSM(),
          }),
          new VectorLayer({
            source: new VectorSource({
              projection: "EPSG: 4326",
              features: [iconFeature],
            }),
            style: new Style({
              image: new Circle({
                radius: 5,
                fill: new Fill({
                  color: "red",
                }),
              }),
            }),
          }),
        ],
        view: new View({
          projection: "EPSG:4326",
          center: [65.34803, 40.101679],
          zoom: 12,
        }),
      });

      return {};
    });
  },
};
</script>
