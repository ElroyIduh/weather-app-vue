<template>
  <h1>Wetter-App</h1>
  <h2>Die beste Wetter App Deutschlands</h2>

  <div class="search-box">
    <input
      class="search-text"
      type="text"
      placeholder="Stadt oder Postleitzahl eingeben :)"
      v-model="cityInput"
      @keyup.enter="searchCity"
    />
    <button class="search-button" @click="searchCity">Search</button>
  </div>

  <div v-if="weatherData">
    <img
      :src="`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`"
      :alt="current.weather[0].description"
    />
    <div v-if="current">
      <Current :current="current" />
    </div>
    <div class="hourly">
      <Hour v-for="hour in hourly" :key="hour.dt" :hour="hour" />
    </div>
    <div class="card-container" v-if="daily">
      <Day v-for="day in daily.slice(0, 4)" :key="day.dt" :day="day" />

      <DailyQuote
        text="  Empty your mind, be formless, shapeless — like water. Now you put water in a cup, it becomes the cup; You put water into a bottle it becomes the bottle; You put it in a teapot it becomes the teapot. Now water can flow or it can crash. Be water, my friend. "
        author="Bruce Lee"
      />

      <Day
        class="day"
        v-for="day in daily.slice(-4)"
        :key="day.dt"
        :day="day"
      />
    </div>
  </div>
</template>

<script>
import Day from "./components/Day";
import Hour from "./components/Hour";
import Current from "./components/Current";
import DailyQuote from "./components/DailyQuote";

export default {
  data() {
    return {
      hourly: null,
      daily: null,
      current: null,
      weatherData: null,
      cityInput: "",
    };
  },
  components: {
    Day,
    Hour,
    Current,
    DailyQuote,
  },
  created() {
    let lat = 48.2629984;
    let lon = 11.4339022;

    navigator.geolocation.getCurrentPosition(
      (position) => {
        lat = position.coords.latitude;
        lon = position.coords.longitude;

        this.getWeatherData(lat, lon);
      },
      (error) => {
        console.error(error);
        this.getWeatherData(lat, lon);
      }
    );
  },
  methods: {
    getWeatherData() {
      const apiKey = process.env.VUE_APP_WEATHER_API_KEY;
      let lat = 48.2629984;
      let lon = 11.4339022;
      const lang = "de";

      let apiUrl = `https://api.openweathermap.org/data/2.5/onecall?appid=${apiKey}&lat=${lat}&lon=${lon}&lang=${lang}&units=metric`;

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          console.log("data:", data);
          this.weatherData = data;
          this.hourly = data.hourly;
          this.hourly.splice(24, this.hourly.length - 1);
          console.log(this.hourly);
          this.daily = data.daily;
          this.current = data.current;
        });
    },

    getCurrentCity() {
      const apiKey = process.env.VUE_APP_GEO_API_KEY;
      let lat = 48.2629984;
      let lon = 11.4339022;
      

      let apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${lat}+${lon}&key=${apiKey}`;
    },

    searchCity() {
      alert(this.cityInput);
    },
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

.hourly {
  display: flex;
  flex-direction: row;
  width: 100%;
  overflow: scroll;
  overflow-y: hidden;
}

.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 4rem;
}

.card {
  flex: 0 32%;
  margin-bottom: 2%;
}

.currentIcon {
  width: 12%;
}

.search-box {
  color: #f7f6f1;
}
.search-text {
  border: none;
  border-bottom: 2px solid hsl(210, 29%, 42%);
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background: none;
  min-width: 16.25rem;
}

.search-text:focus-visible {
  outline: none;
}

.search-text::placeholder {
  color: hsl(210, 29%, 41%);
}

.search-button {
  margin-left: 1rem;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background: #2c3e50;
  color: white;
  border: none;
  border-bottom: 2px solid #2c3e50;
  border-radius: 4px;
  cursor: pointer;
}
</style>
