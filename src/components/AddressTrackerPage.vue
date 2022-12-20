<template>
  <div class="container">
    <div class="header">
      <h2 class="title">IP Address Tracker</h2>
      <div class="input-wrapper">
        <input class="input-search" type="text" v-model="inputIP" />
        <button @click="getCoordinations" class="search">
          <img src="../assets/icon-arrow.svg" alt="arrow" />
        </button>
      </div>

      <div class="content">
        <div class="data">
          <span class="data-title">IP ADDRESS</span>
          <span>{{ inputIP }}</span>
        </div>
        <hr />
        <div class="data">
          <span class="data-title">LOCATION</span>
          <span
            >{{ locationData.location.city}}
            {{ locationData.location.region }} <br />
            {{ locationData.location.postalCode }}</span
          >
        </div>
        <hr />
        <div class="data">
          <span class="data-title">TIMEZONE</span>
          <span>{{ locationData.location.timezone }}</span>
        </div>
        <hr />
        <div class="data">
          <span class="data-title">ISP</span>
          <span>{{ locationData.isp }}</span>
        </div>
      </div>
    </div>
    <div class="map">
      <GoogleMap
        api-key="AIzaSyDivIkCiS_FnVJIDxm4ho2MsxbqcZrqK6E"
        style="width: 100%; height: 100%"
        center="center"
        :zoom="15"
      >
        <Marker :options="{ position: center}" />
      </GoogleMap>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { defineComponent } from "vue";
import { GoogleMap, Marker } from "vue3-google-map";

export default defineComponent({
  components: { GoogleMap, Marker },
  data() {
    return {
      locationData: {
        ip: "",
        location: {
          country: "",
          region: "",
          city: "",
          lat: undefined,
          lng: undefined,
          postalCode: "",
          timezone: "",
          geonameId: undefined,
        },
        isp: "",
      },
      inputIP: "",
    };
  },
  methods: {
    getCoordinations() {
      axios
        .get(
          `https://geo.ipify.org/api/v2/country,city?apiKey=at_K75noHVDRw5fdtjU6yO1VPK1RVUx5&ipAddress=${this.inputIP}`
        )
        .then((response) => {
          console.log(response.data);
          this.$data.locationData.ip = response.data.ip;
          this.$data.locationData.location.country =
            response.data.location.country;
          this.$data.locationData.location.region =
            response.data.location.region;
          this.$data.locationData.location.city = response.data.location.city;
          this.$data.locationData.location.lat = response.data.location.lat;
          this.$data.locationData.location.lng = response.data.location.lng;
          this.$data.locationData.location.postalCode =
            response.data.location.postalCode;
          this.$data.locationData.location.timezone =
            response.data.location.timezone;
          this.$data.locationData.isp = response.data.isp;
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  name: "AddressTrackerPage",
});
</script>

<style>
/*******header**********/
.header {
  background-image: url("../assets/pattern-bg.png");
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  text-align: center;
  height: 200px;
  position: relative;
}

.title {
  color: #fff;
}

.input-wrapper {
  padding-bottom: 50px;
}

.input-search {
  height: 35px;
  border-radius: 10px 0 0 10px;
  border: none;
  width: 350px;
}
.input-search:focus {
  outline: none;
}
.search {
  height: 35px;
  border-radius: 0 10px 10px 0;
  border: none;
  width: 45px;
  padding-bottom: 3px;
  background: #3f3f3f;
  cursor: pointer;
}

/*******contentSection**********/

.content {
  display: flex;
  align-self: center;
  justify-content: space-between;
  position: absolute;
  width: 800px;
  height: 80px;
  background: #fff;
  bottom: -40px;
  z-index: 999;
  border-radius: 10px;
  padding: 20px;
}

.data {
  display: flex;
  flex-direction: column;
}

.data-title {
  font-size: 8px;
  font-weight: 700;
  color: #9f9f9f;
  text-align: left;
  margin-bottom: 5px;
}

/**********mapSection****************/
.map {
  background: black;
  position: relative;
  height: 100vh;
}
iframe {
  width: 100%;
  height: 100%;
}
</style>
