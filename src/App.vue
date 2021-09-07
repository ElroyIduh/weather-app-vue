<template>
  <!-- Loader -->
  <div v-if="loading" class="loader-container">
    <div class="lds-ripple">
      <div></div>
      <div></div>
    </div>
  </div>

  <h1 v-if="!loading">Elroy's Wetter-App</h1>
  <h2 v-if="!loading">Die beste Wetter App Deutschlands</h2>

  <!-- Search teil -->
  <div v-if="!loading" class="search-box">
    <input
      class="search-text"
      type="text"
      :placeholder="city"
      v-model="cityInput"
      @keyup.enter="searchCity"
    />
    <button class="search-button" @click="searchCity">Search</button>
  </div>

  <div v-if="weatherData">
    <div v-if="current">
      <Current :current="current" :city="city" />
    </div>
    <div class="hourly">
      <Hour v-for="hour in hourly" :key="hour.dt" :hour="hour" />
    </div>
    <div class="card-container" v-if="daily">
      
      <Day v-for="day in daily.slice(0, 4)" :key="day.dt" :day="day" />

      <!-- <DailyQuote
        text="  Empty your mind, be formless, shapeless — like water. Now you put water in a cup, it becomes the cup; You put water into a bottle it becomes the bottle; You put it in a teapot it becomes the teapot. Now water can flow or it can crash. Be water, my friend. "
        author="Bruce Lee"
      /> -->

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
      city: "",
      loading: false,
    };
  },
  components: {
    Day,
    Hour,
    Current,
    DailyQuote,
  },
  created() {
    this.loading = true;
    let lat = 48.2629984;
    let lon = 11.4339022;

    navigator.geolocation.getCurrentPosition(
      (position) => {
        lat = position.coords.latitude;
        lon = position.coords.longitude;

        this.getWeatherData(lat, lon);
        this.getCurrentCity(lat, lon);
      },
      (error) => {
        console.error(error);
        this.getWeatherData(lat, lon);
        this.getCurrentCity(lat, lon);
      }
    );
  },
  methods: {
    getWeatherData(lat, lon) {
      this.loading = true;
      const apiKey = process.env.VUE_APP_WEATHER_API_KEY;
      const lang = "de";

      let apiUrl = `https://api.openweathermap.org/data/2.5/onecall?appid=${apiKey}&lat=${lat}&lon=${lon}&lang=${lang}&units=metric`;

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          console.log("weatherData:", data);
          this.weatherData = data;
          this.hourly = data.hourly;
          this.hourly.splice(24, this.hourly.length - 1);
          console.log(this.hourly);
          this.daily = data.daily;
          this.current = data.current;
          this.loading = false;
        });
    },

    getCurrentCity(lat, lon) {
      const apiKey = process.env.VUE_APP_GEO_API_KEY;

      let apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${lat}+${lon}&key=${apiKey}`;

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          console.log("OpenCageData", data);

          const locationComponents = data.results[0].components;

          if (locationComponents.city) {
            this.city = locationComponents.city;
          } else if (locationComponents.town) {
            this.city = locationComponents.town;
          } else {
            this.city = locationComponents.village;
          }
        });
    },

    searchCity() {
      const apiKey = process.env.VUE_APP_GEO_API_KEY;

      let apiUrl = `https://api.opencagedata.com/geocode/v1/json?q=${this.cityInput}&key=${apiKey}`;

      // alert(apiUrl)

      fetch(apiUrl)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          const lat = data.results[0].geometry.lat;
          const lon = data.results[0].geometry.lng;

          this.getWeatherData(lat, lon);

          const locationComponents = data.results[0].components;
          if (locationComponents.city) {
            this.city = locationComponents.city;
          } else if (locationComponents.town) {
            this.city = locationComponents.town;
          } else {
            this.city = locationComponents.village;
          }

          this.cityInput = "";
        });
    },
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.hourly {
  display: flex;
  flex-direction: row;
  width: 100%;
  overflow: scroll;
  overflow-y: hidden;
  box-sizing: border-box;
  border-radius: 6px;
}

/*
.card-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin: 4rem;
  padding: 3rem;
}
*/

.card-container {
  margin: 1rem;
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
}

/*
.card {
  flex: 0 32%;
  margin-bottom: 2%;
}
*/

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
  /*
  min-width: 16.25rem;
  */
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

.hourly {
  padding: 3rem;
}

/* Loader */

.loader-container,
:root {
  --scale: 3;
}

.loader-container {
  height: 100vh;

  display: flex;
  justify-content: center;
  align-items: center;
}

.lds-ripple {
  display: inline-block;
  position: relative;
  width: calc(80px * var(--scale));
  height: calc(80px * var(--scale));
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #fff;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: calc(36px * var(--scale));
    left: calc(36px * var(--scale));
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0px;
    left: 0px;
    width: calc(72px * var(--scale));
    height: calc(72px * var(--scale));
    opacity: 0;
  }
}

/* display: flex;
  justify-content: center;
  align-items: center;
}

.lds-ripple {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ripple div {
  position: absolute;
  border: 4px solid #fff;
  opacity: 1;
  border-radius: 50%;
  animation: lds-ripple 1s cubic-bezier(0, 0.2, 0.8, 1) infinite;
}
.lds-ripple div:nth-child(2) {
  animation-delay: -0.5s;
}
@keyframes lds-ripple {
  0% {
    top: 72px;
    left: 36px;
    width: 0;
    height: 0;
    opacity: 1;
  }
  100% {
    top: 0px;
    left: 0px;
    width: 72px;
    height: 72px;
    opacity: 0;
  }
} */
</style>
