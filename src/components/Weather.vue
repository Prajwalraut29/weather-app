<template>
  <div class="container">
    <div class="d-flex">
      <div class="card main-div w-100">
        <div class="p-3">
          <h2 class="mb-1 day">Today</h2>
          <p class="date mb-0">{{ date }}</p>
          <small>{{ time }}</small>
          <h2 class="place">
            <i class="fa fa-location"
              >{{ name }} <small>{{ country }}</small></i
            >
          </h2>
          <div class="temp">
            <h1 class="weather-temp">{{ temperature }}&deg;</h1>
            <h2 class="text">{{ description }} <img :src="iconUrl" /></h2>
          </div>
          <input
            @click="changeLocation"
            type="button"
            value="Change Location"
            class="btn change-btn btn-primary"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "myWeather",
  components: {},
  props: {
    city: String,
  },
  data() {
    return {
      temperature: null,
      description: null,
      iconUrl: null,
      date: null,
      time: null,
      monthNames: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ],
      methods: {
        changeLocation() {
          window.location.reload();
        },
      },
    };
  },
  async created() {
    const response = await axios.get(
      `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=819b752718972625466161062e51636f`
    );
    console.log(response);
    const weatherData = response.data;
    this.temperature = weatherData.main.temp;
    this.description = weatherData.weather[0].description;
    this.name = weatherData.name;
    const d = new Date();
    this.date =
      d.getDate() + "-" + this.monthNames[d.getMonth()] + "-" + d.getFullYear();
    this.time =
      d.getHours() + "-" + "-" + d.getMinutes() + ":" + d.getSeconds();
    this.iconUrl = `https://api.openweathermap.org/img/w/${weatherData.weather[0].icon}.png`;
  },
};
</script>

<style>
body {
  background-color: #121212;
}

.box {
  background-color: aqua;
}
</style>
