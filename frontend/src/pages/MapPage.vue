<template>
  <q-page class="row items-center justify-evenly">
    <maplibre-map
      position
      geocoder
      :zoom="2"
      @map:loaded="onMapLoaded"
      @map:click="onMapClick"  />
  </q-page>
</template>

<script setup lang="ts">
import MaplibreMap from 'components/MaplibreMap.vue';
import { Map, MapMouseEvent } from 'maplibre-gl';

const mapStore = useMapStore();
const filtersStore = useFiltersStore();

function onMapLoaded(map: Map) {
  mapStore.initLayers(map).then(() => {
    mapStore.applyFilters(filtersStore.asParams());
  });
}

function onMapClick(event: MapMouseEvent) {
  console.log('Map clicked at:', event.lngLat);
  // custom popup
  // new Popup()
  //   .setLngLat(event.lngLat)
  //   .setHTML('<b>Hello World!</b>')
  //   .addTo(map as Map);
}
</script>
