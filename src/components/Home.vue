<template>

<div>
    <Header></Header>

  <!-- <GoogleMapLoader
    :mapConfig="mapConfig"
    apiKey="AIzaSyD7yHU3hoFHGh8liZIAHJTBUn_Ld7IYTaE"
  > -->
    <!-- <template slot-scope="{ google, map }">
      <GoogleMapMarker @click.native="hola"
        v-for="marker in $store.state.markers"
        :key="marker.id"
        :marker="marker"
        :google="google"
        :map="map"
      /> -->
     <div><GmapMap
    :center="{lat:$store.state.latitude, lng:$store.state.longitude}"
    :zoom="15"
   :options="mapSettings"
    style="width: 100%; height: 100vh;"
    >
 <GmapMarker   
    :key="marker.id"
   v-for="marker in $store.state.markers"
    :position="marker.position"
    :clickable="true"
    :draggable="false"
    :icon="icon"
    @click="toggleInfoWindow(marker,marker.id)"
  />
  <GmapMarker   
    :position="{lat:  $store.state.latitude,lng: $store.state.longitude}"
    :clickable="true"
    :draggable="false"
    :icon="userIcon"
    @click="toggleInfoWindow(marker,marker.id)"
  />
  <GmapInfoWindow
       :options="infoOptions"
        :position="infoWindowPos"
        :opened="infoWinOpen"
        
        @closeclick="infoWinOpen=false"
      >
        <MapInfoWindow :marker="currentMarker"/>

         </GmapInfoWindow>
</GmapMap></div>
    
  
  <!-- </GoogleMapLoader> -->
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import MapInfoWindow from '@/components/MapInfoWindow.vue'

// import GoogleMapLoader from "./GoogleMapLoader";
// import GoogleMapMarker from "./GoogleMapMarker";
import { POINT_MARKER_ICON_CONFIG } from "@/constants/mapSettings";
import { POINT_MARKER_USER_ICON_CONFIG } from "@/constants/mapSettings";
 import { mapSettings } from "@/constants/mapSettings";

export default {
  components: {
    // GoogleMapLoader,
    // GoogleMapMarker,
    MapInfoWindow,
    Header
  },

  data() {
    return {
        icon: POINT_MARKER_ICON_CONFIG,
        userIcon: POINT_MARKER_USER_ICON_CONFIG,
        mapSettings: mapSettings,
         infoWinOpen: false,
         currentMarker: {},
      infoOptions: {
          maxWidth : '250',
          pixelOffset: {
            width: 0,
            height: -35
          }
        },
         infoContent: '',
        
        infoWindowPos: {
          lat: 0,
          lng: 0
        },
    };
  },
   mounted() {
      //set bounds of the map
      this.$store.dispatch('getPosition')
     
    },
methods:{
   
    toggleInfoWindow(marker, idx){
        this.infoWindowPos = marker.position;
        this.infoContent = this.getInfoWindowContent(marker);
        

        //check if its the same marker that was selected if yes toggle
        if (this.currentMidx == idx) {
          this.infoWinOpen = !this.infoWinOpen;
        }
        //if different marker set infowindow to open and reset current marker index
        else {
          this.infoWinOpen = true;
          this.currentMidx = idx;
        }
    }, getInfoWindowContent(marker){
      this.currentMarker = marker
        //return (
        
          // `<div class="card">
          //       <div class="card-image"  style="overflow-x: auto; display: flex; width: 200px;height: 100px;">
          //           <figure  class="image is-4by3">
          //           <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
          //           <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
          //           <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
          //           <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
          //           <img src="https://bulma.io/images/placeholders/96x96.png" alt="Placeholder image">
          //           </figure>
          //       </div>
          //       <div class="card-content">
          //           <div class="media">
          //           <div class="media-content">
          //               <p class="title is-4">${marker.title}</p>
          //               <p class="title is-4">${marker.address}</p>
          //           </div>
          //           </div>
          //           <a href="/bar/${marker.id}/reservas">RESERVAR</a>
          //           <div class="content">
          //       </div>
          //       </div>`
          //      );
    }
}
}
</script>
<style>
   .vue-map-container {
  position: relative;
}

.vue-map-container .vue-map {
  left: 0; right: 0; top: 0; bottom: 0;
  position: absolute;
}

.vue-map-hidden {
  display: none;
}
</style>