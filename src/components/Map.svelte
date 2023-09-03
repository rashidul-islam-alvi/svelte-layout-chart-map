<script>
  import { onMount } from "svelte";
  import TileLayer from "ol/layer/Tile.js";
  import Map from "ol/Map";
  import OSM from "ol/source/OSM.js";
  import View from "ol/View";
  import { fromLonLat } from "ol/proj";
  import VectorLayer from "ol/layer/Vector";
  import VectorSource from "ol/source/Vector";
  import GeoJSON from "ol/format/GeoJSON";
  import Style from "ol/style/Style";
  import Fill from "ol/style/Fill";
  import Stroke from "ol/style/Stroke";
  /**
   * @type {Map}
   */
  let map;

  onMount(() => {
    const geoJSONStyle = new Style({
      fill: new Fill({
        color: "#006a4e",
        // Set the color to #006a4e and opacity to 0.75
      }),
      stroke: new Stroke({
        color: "white",
      }),
    });

    // Initialize the map
    map = new Map({
      target: "map", // The ID of the map container
      layers: [
        new TileLayer({
          source: new OSM(), // OpenStreetMap as the base layer
        }),
        new VectorLayer({
          source: new VectorSource({
            format: new GeoJSON(),
            url: "./countries.geojson",
          }),
          style: geoJSONStyle,
        }),
      ],
      view: new View({
        center: fromLonLat([0, 0]), // Center the map at (0,0)
        zoom: 2, // Initial zoom level
      }),
    });
  });
</script>

<div id="map" />

<style>
  /* Apply full-screen styles to the map container */
  #map {
    width: 100%;
    height: 100vh; /* 100% of the viewport height */
  }
</style>
