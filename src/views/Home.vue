<template>
  <div class="home">
    <h1>This is home page</h1>
    <label for="location">Location: </label>
    <input type="text" v-model="location" id="location" /><button
      @click="fetchWeather"
    >
      Fetch
    </button>
    <h1>{{ weather.name }}</h1>
    <h1>{{ weather.weather[0].main }}</h1>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
let weatherAPI = process.env.VUE_APP_TEST_KEY;
export default {
  name: "Home",
  components: {},
  data() {
    return {
      location: "",
      weather: { weather: [{ main: "" }], name: "" },
    };
  },
  methods: {
    fetchWeather() {
      if (this.location) {
        axios
          .get(
            `https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=${weatherAPI}`
          )
          .then((response) => {
            console.log(response.data);
            this.weather = response.data;
            console.log(this.weather.weather[0].main);
          });
      }
    },
  },
};
</script>
