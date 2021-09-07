<template>
  <div class="current">
    <div class="card-current">
      <h3>{{ getTime(current.dt) }}</h3>
      <img
        :src="`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`"
        :alt="current.weather[0].description"
      />
      <h3>Aktuelles Wetter in {{ city }}</h3>
      <!-- <p>{{ getDate(current.dt) }} </p> -->
      <p>{{ current.weather[0].description }}</p>

      <!-- 4° Schnee Icon (<i class="fas fa-snowflake"></i>)
    5-11° Tiefe Temperatur (<i class="fas fa-thermometer-quarter"></i>)
    12-22° Normale Temperatur (<i class="fas fa-thermometer-half"></i>)
    23- open end° hohe Temperatur (<i class="fas fa-thermometer-full"></i>) 
    -->
      <p>
        <i v-if="current.temp <= 5" class="fas fa-snowflake"></i>
        <i v-if="current.temp >=5 && current.temp <=11" class="fas fa-thermometer-quarter"></i>
        <i v-if="current.temp >=12 && current.temp <=22" class="fas fa-thermometer-half"></i>
        <i v-if="current.temp >= 23" class="fas fa-thermometer-full"></i>
        {{ formatCurrentTermperature(current.temp) }}
      </p>
      <p>
        <i class="fas fa-wind"></i> {{ formatWindspeed(current.wind_speed) }}
      </p>
      <p>
        <i class="fas fa-humidity"></i> {{ formatHumidity(current.humidity) }} %
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["quote", "current", "city"],
  methods: {
    getDate(dt) {
      const date = new Date(dt * 1000);

      const month = "0" + (date.getMonth() + 1);
      const day = "0" + date.getDate();
      const year = date.getFullYear();

      const formattedDate =
        day.substr(-2) + "." + month.substr(-2) + "." + year;

      return formattedDate;
    },
    getTime(dt) {
      const date = new Date(dt * 1000);
      const hours = date.getHours();
      const minutes = "0" + date.getMinutes();

      const formattedTime = hours + ":" + minutes.substr(-2);

      return formattedTime;
    },
    formatCurrentTermperature(temp) {
      const roundedTemp = Math.round(temp);
      return `${roundedTemp} °C`;
    },
    formatWindspeed(wind_speed) {
      const windSpeed = Math.round(wind_speed * 3.6 * 10) / 10;
      return `${windSpeed} km/h`;
    },
    formatHumidity(humidity) {
      const humidityLevel = humidity;
      return ` ${humidityLevel}`;
    },
  },
};
</script>

<style>
.current {
  padding: 3rem;
  padding-top: 6rem;
  font-size: 25px;
}
.card-current {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: 95%;
  border-radius: 5px;
  margin: 0 auto;
  padding: 5px;
}
.card-current:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
</style>