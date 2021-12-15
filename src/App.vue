<template>
  <div id="app">
    <header>
      <div class="header flex flex-col items-center w-full relative">
        <h1 class="text-3xl text-white font-bold my-10">IP Address Tracker</h1>
        <div>
          <form @submit.prevent class="w-full rounded-xl flex overflow-hidden">
            <input type="text" class="py-1 px-4 h-14 text-xl" placeholder="Search for any IP address or domain" v-model="searchInput" name="ip">
            <div class="bg-black flex justify-center items-center px-5 py-2 cursor-pointer" @click="searchIp">
              <img src="./assets/images/icon-arrow.svg" alt="" class="pointer-events-none">
            </div>
          </form>
        </div>
      </div>
      <div class="results absolute rounded-xl border border-black bg-white flex w-3/4 px-5 py-10 z-10">
        <div class="flex flex-col relative items-start" id="ipAdress">
          <h1 class="text-gray-600 font-bold mb-4 mr-32">IP ADDRESS</h1>
          <p class="text-xl font-bold text-black">{{data.ip}}</p>
        </div>
        <div class="flex flex-col relative items-start mr-32" id="location">
          <h1 class="text-gray-600 font-bold mb-4">LOCATION</h1>
          <p class="text-xl font-bold text-black">{{data.location.city}}</p>
        </div>
        <div class="flex flex-col relative items-start mr-32" id="timezone">
          <h1 class="text-gray-600 font-bold mb-4">TIMEZONE</h1>
          <p class="text-xl font-bold text-black">{{data.location.timezone}}</p>
        </div>
        <div class="flex flex-col relative items-start">
          <h1 class="text-gray-600 font-bold mb-4">ISP</h1>
          <p class="text-xl font-bold text-black">{{data.isp}}</p>
        </div>
      </div>
    </header>
    <div class="h-96 w-full relative z-0">
      <l-map class="w-full" :center="center" :zoom="zoom" id="myMap">
        <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
          <l-marker :lat-lng="markerLatLng" :icon="icon">
          </l-marker>
      </l-map>
    </div>
  </div>
</template>

<script>
import axios from "axios"
// import { latLng } from "leaflet";
import { LMap, LTileLayer, LMarker } from "vue2-leaflet";
import "leaflet/dist/leaflet.css";
import { Icon } from 'leaflet';


export default {
  name: 'App',
  data(){
    return {
      result: null,
      searchInput: "",
      zoom: 13,
      attribution: '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      center: null,
      markerLatLng: null,
    }
  },
  components: {
    LMap,
    LTileLayer,
    LMarker,
    // LTooltip
  },
  methods: {
    searchIp(){
      axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=at_8fc4RU4wQAlLBY6mAHc0aMY1bQb7z&ipAddress=${this.searchInput}`)
        .then(response => {
          this.result = response.data;
          this.center = [this.result.location.lat, this.result.location.lng];
          this.markerLatLng = [this.result.location.lat, this.result.location.lng];
        })
    }
  },
  computed: {
    data: function () {
      if(this.result == "null") {
        return this.result;
      } else {
        return this.result;
      }
    },
    url(){
      return 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png'
    }
  },
  mounted(){
    axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=at_8fc4RU4wQAlLBY6mAHc0aMY1bQb7z&ipAddress=94.110.7.98`)
      .then(response => {
        this.result = response.data;
        console.log(this.result);
        this.center = [this.result.location.lat, this.result.location.lng];
        this.markerLatLng = [this.result.location.lat, this.result.location.lng];
      });
    delete Icon.Default.prototype._getIconUrl;
    Icon.Default.mergeOptions({
      iconRetinaUrl: require('leaflet/dist/images/marker-icon-2x.png'),
      iconUrl: require('leaflet/dist/images/marker-icon.png'),
      shadowUrl: require('leaflet/dist/images/marker-shadow.png'),
});

  },
  
}

</script>

<style>
#app {
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.header {
  background-image: url("./assets/images/pattern-bg.png");
  background-repeat: no-repeat;
  background-size: cover;
  height: 280px
}

form input{
  width: 600px
}

.results{
  height: 170px;
  top: 30%;
  left: 12%;
}

#ipAdress::after, #location::after, #timezone::after{
  content: "";
  width: 1px;
  height: 80px;
  background-color: lightgray;
  position: absolute;
  left: 200px;
  top: 10px
}


#map {
  height: 200px
}

</style>
