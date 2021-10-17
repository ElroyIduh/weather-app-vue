<template>
  <div class="current">
    <div class="card-current">
      <h3>{{ getTime(current.dt) }}</h3>
      <img
        :src="`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`"
        :alt="current.weather[0].description"
      />
      <h3>Aktuelles Wetter in {{ city }}</h3>
  
      <p>{{ current.weather[0].description }}</p>

   
      <p>
        <i v-if="current.temp <= 1" class="fas fa-snowflake"></i>
        <i v-if="current.temp >=1 && current.temp <=12" class="fas fa-thermometer-quarter"></i>
        <i v-if="current.temp >12 && current.temp <=23" class="fas fa-thermometer-half"></i>
        <i v-if="current.temp >= 23" class="fas fa-thermometer-full"></i>
        {{ formatCurrentTermperature(current.temp) }}
      </p>
      <p>
        <i class="fas fa-wind"></i> {{ formatWindspeed(current.wind_speed) }}
      </p>
      <p>
        <svg width="1em" height="1em" viewBox="0 0 1467 2134" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;fill: #2c3e50;clip-rule:evenodd;stroke-linejoin:round;stroke-miterlimit:2;"><path d="M855.083,92.042c-33.083,-119.917 -206,-125.5 -243.5,-0c-194.875,657.333 -611.583,835.958 -611.583,1299.25c0,410.166 328,742.041 733.333,742.041c405.334,0 733.334,-331.875 733.334,-742.041c-0,-465.625 -415.792,-638.917 -611.584,-1299.25Zm144.103,1416.28c-33.856,0.201 -67.652,13.216 -93.479,39.043c-1.219,1.218 -2.408,2.454 -3.575,3.713l-0.579,0.629c-47.869,52.305 -46.486,133.576 4.154,184.216c52.061,52.061 136.496,52.061 188.557,-0c41.718,-41.701 50.02,-104.16 24.903,-154.14c-6.236,-12.409 -14.538,-24.054 -24.903,-34.418c-25.827,-25.827 -59.623,-38.842 -93.479,-39.043l-0.8,-0.003l-0.799,0.003Zm-4.029,-509.74c-16.791,0.199 -33.519,6.708 -46.326,19.526l-572.382,572.381c-26.041,26.041 -26.041,68.248 0,94.268l47.124,47.124c13.02,13.021 30.082,19.531 47.142,19.531l0.8,-0.005c16.791,-0.2 33.519,-6.708 46.326,-19.526l572.382,-572.381c24.877,-24.857 25.989,-64.487 3.334,-90.683c-1.058,-1.225 -2.17,-2.422 -3.334,-3.586l-47.124,-47.123c-12.817,-12.818 -29.551,-19.327 -46.342,-19.526l-0.8,-0.005l-0.8,0.005Zm-529.291,-23.58c-33.856,0.201 -67.652,13.216 -93.479,39.043c-24.027,24.026 -36.965,54.948 -38.814,86.401c-2.159,36.699 10.779,74.122 38.814,102.157c26.041,26.041 60.165,39.061 94.286,39.061l0.8,-0.002c22.53,-0.134 45.031,-5.945 65.178,-17.435c10.129,-5.777 19.656,-12.984 28.293,-21.624c42.352,-42.352 50.251,-106.128 23.694,-156.475c-6.086,-11.538 -13.984,-22.373 -23.694,-32.083c-8.965,-8.965 -18.889,-16.386 -29.442,-22.262l-0.661,-0.366c-7.202,-3.957 -14.692,-7.198 -22.361,-9.723l-0.768,-0.251c-0.257,-0.081 -0.513,-0.163 -0.769,-0.245l-0.771,-0.241c-0.257,-0.078 -0.514,-0.157 -0.771,-0.236c-1.544,-0.467 -3.095,-0.905 -4.652,-1.315c-0.776,-0.205 -1.554,-0.402 -2.339,-0.594l-0.782,-0.188c-0.784,-0.186 -1.569,-0.365 -2.35,-0.536l-0.785,-0.169l-0.786,-0.165c-8.651,-1.782 -17.444,-2.7 -26.242,-2.752l-0.799,-0.003l-0.8,0.003Z"/></svg> {{ formatHumidity(current.humidity) }} %
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