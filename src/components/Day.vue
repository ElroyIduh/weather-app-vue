<template>
  <!-- Cards und Card Input -->
  <div class="card">
    <img
      :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`"
      :alt="day.weather[0].description"
    />
    <div>
      <p>{{ getDay(day.dt) }} - {{ getDate(day.dt) }}</p>
      <p>
        <i class="fas fa-thermometer-quarter"></i>
        {{ formatTermperature(day.temp.min) }}
      </p>
      <p>
        <i class="fas fa-thermometer-half"></i>
        {{ formatTermperature(day.temp.max) }}
      </p>
      <p><i class="fas fa-wind"></i> {{ formatWindspeed(day.wind_speed) }}</p>
      <p>
        <i class="fas fa-humidity"></i> {{ formatHumidity(day.humidity) }} %
      </p>

      <p v-if="day.rain">
        <i class="fas fa-cloud-rain"></i> {{ formatRain(day.rain) }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["day"],
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
    getDay(dt) {
      const days = ["SO", "MO", "DI", "MI", "DO", "FR", "SA"];

      const date = new Date(dt * 1000);

      const dayNumber = date.getDay();
      return days[dayNumber];
    },
    formatTermperature(temp) {
      const roundedTemp = Math.round(temp);
      return `${roundedTemp} °C`;
    },
    formatRain(rain) {
      const rainProbability = rain;
      return ` ${rainProbability} %`;
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
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  border-radius: 5px;
}
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
/* .container {
  padding: 2px 16px;
  
} */
</style>