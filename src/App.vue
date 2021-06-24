<template>
  <h1>Weather-app</h1>
  <h2>The best weather app in germany</h2>
  <div v-if="weatherData">
    <img
      :src="`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`"
      :alt="current.weather[0].description"
    />
    <div v-if="current">
      <Current :current="current" quote="quote of the day" />
    </div>
    <div v-if="daily">
      <Day v-for="day in daily" :key="day.dt" :day="day" />
    </div>

  <div v-if="dailyquote">
      <!-- <DailyQuote text=" Empty your mind, be formless, shapeless — like water. Now you put water in a cup, it becomes the cup; You put water into a bottle it becomes the bottle; You put it in a teapot it becomes the teapot. Now water can flow or it can crash. Be water, my friend. " author="Bruce Lee" /> -->
  </div>
    
  </div>
</template>

<script>
import Day from "./components/Day";
import Current from "./components/Current";
import DailyQuote from ".components/DailyQuote";

export default {
  data() {
    return {
      hourly: null,
      daily: null,
      current: null,
      weatherData: null,
    };
  },
  components: {
    Day,
    Current,
    DailyQuote,
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
