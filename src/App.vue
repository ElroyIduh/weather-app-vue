<template>
  <h1>Weather-app</h1>
  <h2>The best weather app in germany</h2>
  <img alt="Vue logo" src="./assets/logo.png" />
  <div v-if="current">
    <h1>Current</h1>
    <p>{{ current.dt }}</p>
    <p>{{ current.weather[0].description }}</p>
  </div>
  <div v-if="daily">
    <div v-for="day in daily" :key="day.dt">
      <h2>{{ day.dt }}</h2>
      <h2>{{ day.temp.day }}</h2>
      <h2>{{ day.temp.min }}</h2>
      <h2>{{ day.temp.max }}</h2>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hourly: null,
      daily: null,
      current: null,
      weatherData: null,
    };
  },
  created() {
    const apiKey = process.env.VUE_APP_WEATHER_API_KEY;
    const lat = 48.2629984;
    const lon = 11.4339022;
    const lang = "de";

    let apiUrl = `https://api.openweathermap.org/data/2.5/onecall?appid=${apiKey}&lat=${lat}&lon=${lon}&lang=${lang}&units=metric`;

    fetch(apiUrl)
      .then((response) => response.json())
      .then((data) => {
        console.log("data:", data);
        this.weatherData = data;
        this.hourly = data.hourly;
        this.daily = data.daily;
        this.current = data.current;
      });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
