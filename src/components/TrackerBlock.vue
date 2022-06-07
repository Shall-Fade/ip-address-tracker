<template>
  <div class="tracker-container">
    <section class="tracker-section">
      <div class="wrapper">
        <h1 class="main-title">IP Address Tracker</h1>
        <form @submit.prevent="getIpInfo" class="form-group">
          <input
            required
            v-model="ipAddress"
            class="tracker-input"
            type="text"
            placeholder="Search for any IP address or domain"
            pattern="((^|\.)((25[0-5])|(2[0-4]\d)|(1\d\d)|([1-9]?\d))){4}$"
          />
          <button type="submit" class="tracker-btn">
            <img src="../assets/images/icon-arrow.svg" alt="Arrow" />
          </button>
        </form>
      </div>
      <ResultBlock :ipInfo="ipInfo" />
    </section>
    <section class="tracker-map-section">
      <div id="map"></div>
    </section>
  </div>
</template>

<script>
import leaflet from "leaflet";
import axios from "axios";
import { ref, onMounted } from "vue";
import ResultBlock from "./ResultBlock.vue";
export default {
  components: {
    ResultBlock,
  },
  setup() {
    // Variables
    let map;
    const ipAddress = ref("");
    const ipInfo = ref({
      ip: null,
      country: null,
      region: null,
      timezone: null,
      isp: null,
      lat: null,
      lng: null,
    });

    onMounted(() => {
      getMyIpInfo();
    });

    // Get my IP data and display it
    function getMyIpInfo() {
      axios
        .get(
          `https://geo.ipify.org/api/v2/country,city?apiKey=at_OxG3bG7s2Q7xTGZZOnbKEgBs3Vq7X`
        )
        .then((responce) => {
          ipInfo.value = {
            ip: responce.data.ip,
            country: responce.data.location.country,
            region: responce.data.location.region,
            timezone: responce.data.location.timezone,
            isp: responce.data.isp,
            lat: responce.data.location.lat,
            lng: responce.data.location.lng,
          };
          // Coordinates
          map = L.map("map").setView([ipInfo.value.lat, ipInfo.value.lng], 13);
          // Marker
          leaflet.marker([ipInfo.value.lat, ipInfo.value.lng]).addTo(map);
          // Map
          L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
            maxZoom: 19,
            attribution: "© OpenStreetMap",
          }).addTo(map);
        });
    }

    // Get IP data and display it
    function getIpInfo() {
      if (ipAddress.value !== "") {
        axios
          .get(
            `https://geo.ipify.org/api/v2/country,city?apiKey=at_OxG3bG7s2Q7xTGZZOnbKEgBs3Vq7X&ipAddress=${ipAddress.value}`
          )
          .then((responce) => {
            ipInfo.value = {
              ip: responce.data.ip,
              country: responce.data.location.country,
              region: responce.data.location.region,
              timezone: responce.data.location.timezone,
              isp: responce.data.isp,
              lat: responce.data.location.lat,
              lng: responce.data.location.lng,
            };
            // Coordinates
            map.setView([ipInfo.value.lat, ipInfo.value.lng], 13);
            // Marker
            leaflet.marker([ipInfo.value.lat, ipInfo.value.lng]).addTo(map);
          });

        ipAddress.value = "";
      }
    }

    return {
      ipAddress,
      ipInfo,
      getIpInfo,
    };
  },
};
</script>

<style scoped>
.tracker-container {
  height: 100vh;
}
.tracker-section {
  display: flex;
  text-align: center;
  background-image: url("../assets/images/pattern-bg.png");
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  padding-bottom: 150px;
  min-height: 30vh;
  z-index: 20;
}

.main-title {
  font-weight: 500;
  color: var(--c-white);
  padding: 30px 0 20px 0;
}

input,
button {
  border: none;
  outline: none;
  background: none;
}
.form-group {
  width: 600px;
  position: relative;
}
.tracker-input {
  font-family: "Rubik", sans-serif;
  width: 100%;
  background-color: #fff;
  color: var(--c-vary-dark-gray);
  font-weight: 400;
  padding: 20px;
  font-size: 18px;
  border-radius: 15px;
}
.tracker-input::placeholder {
  color: var(--c-dark-gray);
  font-weight: 500;
}
.tracker-btn {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: 0;
  right: 0;
  height: 100%;
  cursor: pointer;
  background-color: #000;
  padding: 25px;
  border-radius: 0 15px 15px 0;
  transition: 0.3s ease;
}
.tracker-btn:hover {
  background-color: var(--c-very-dark-gray);
  transition: 0.3s ease;
}
.tracker-map-section {
  z-index: 10;
  height: 70vh;
}
#map {
  height: 100%;
}

@media only screen and (max-width: 768px) {
  .form-group {
    width: 500px;
    margin: 0 auto;
  }
}
@media only screen and (max-width: 425px) {
  .form-group {
    width: 350px;
    margin: 0 auto;
  }
}
</style>
