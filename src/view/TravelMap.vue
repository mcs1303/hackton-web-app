<template>
    <GoogleMapLoader
      :mapConfig="mapConfig"
      apiKey="AIzaSyCQXGaCgiPDdJY_T4UdqZae3u1LeIsBtmc"
    >
    // insert your google maps api key to render styled map
      <template :slot-scope="{ google, map }">
        <GoogleMapMarker
          v-for="marker in markers"
          :key="marker.id"
          :marker="marker"
          :google="google"
          :map="map"
        />
        <GoogleMapLine
          v-for="line in lines"
          :key="line.id"
          :v-model="line.path"
          :google="google"
          :map="map"
        />
      </template>
    </GoogleMapLoader>
  </template>
  
  <script>
  import GoogleMapLoader from '../components/GoogleMapLoader.vue'
  import GoogleMapMarker from '../components/GoogleMapMarker.vue';
  import GoogleMapLine from '../components/GoogleMapLine.vue';
  
  import { mapSettings } from '../service/mapSettings';
  
  export default {
    components: {
      GoogleMapLoader,
      GoogleMapMarker,
      GoogleMapLine
    },
  
    data() {
      return {
        markers: [
          {
            id: "a",
            position: { lat: 3, lng: 101 }
          },
          {
            id: "b",
            position: { lat: 5, lng: 99 }
          },
          {
            id: "c",
            position: { lat: 6, lng: 97 }
          }
        ],
        lines: [
          {
            id: "1",
            path: [{ lat: 3, lng: 101 }, { lat: 5, lng: 99 }]
          },
          {
            id: "2",
            path: [{ lat: 5, lng: 99 }, { lat: 6, lng: 97 }]
          }
        ]
      };
    },
  
    computed: {
      mapConfig() {
        return {
          ...mapSettings,
          center: this.mapCenter
        };
      },
  
      mapCenter() {
        return this.markers[1].position;
      }
    }
  };
  </script>
  