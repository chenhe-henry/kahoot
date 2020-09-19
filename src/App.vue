<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-toolbar-title v-show="weather"
        >Vue Todo App {{ weather.weather[0].main }}</v-toolbar-title
      >
      <v-spacer></v-spacer>
      <v-btn
        v-for="link in links"
        :key="link.label"
        :to="link.url"
        text
        rounded
        >{{ link.label }}</v-btn
      >
    </v-app-bar>
    <v-content>
      <router-view></router-view>
    </v-content>

    <v-footer color="primary lighten-1" padless>
      <v-row justify="center" no-gutters>
        <v-btn
          v-for="link in links"
          :to="link.url"
          :key="link.label"
          color="white"
          text
          rounded
          class="my-2"
        >
          {{ link.label }}
        </v-btn>
        <v-col class="primary lighten-2 py-4 text-center white--text" cols="12">
          {{ new Date().getFullYear() }} — <strong>Vue Todo App</strong>
        </v-col>
      </v-row>
    </v-footer></v-app
  >
</template>

<script>
import axios from "axios";
let weatherAPI = process.env.VUE_APP_TEST_KEY;
export default {
  name: "App",

  components: {},

  data: () => ({
    links: [
      { label: "Home", url: "/" },
      { label: "About", url: "/about" },
      { label: "Todos", url: "/todos" },
    ],
    weather: null,
  }),
  created() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/weather?q=Sydney&appid=${weatherAPI}`
      )
      .then((response) => {
        console.log(response.data);
        this.weather = response.data;
        console.log(this.weather.weather[0].main);
      });
  },
};
</script>
