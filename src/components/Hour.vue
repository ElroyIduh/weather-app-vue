<template>
<div class = "card-hour">
  <div v-if="hour" class="hour">
    <img
      :src="`http://openweathermap.org/img/wn/${hour.weather[0].icon}@2x.png`"
      :alt="hour.weather[0].description"
    />
    <p>{{ getTime(hour.dt) }}</p>
    <p class="description">
      {{ hour.weather[0].description }}
    </p>
    <p> <i v-if="hour.temp < 5" class="fas fa-snowflake"></i>
        <i v-if="hour.temp >=5 && hour.temp <=12" class="fas fa-thermometer-quarter"></i>
        <i v-if="hour.temp >12 && hour.temp < 23" class="fas fa-thermometer-half"></i>
        <i v-if="hour.temp >= 23" class="fas fa-thermometer-full"></i> {{ formatTermperature(hour.temp) }}</p>

   

   
  </div>
  </div>
</template>

<script>
export default {
  props: ["hour"],
  methods: {
    getTime(dt) {
      const date = new Date(dt * 1000);
      const hours = date.getHours();
      const minutes = "0" + date.getMinutes();

      const formattedTime = hours + ":" + minutes.substr(-2);

      return formattedTime;
    },
    formatTermperature(temp) {
      const roundedTemp = Math.round(temp);
      return `${roundedTemp} °C`;
    },
 
  },
};
</script>

<style>
.hour {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 30%;
  min-width: 165px;
  outline-style: inherit;
  outline-color: ivory;
  align-items: center;
  justify-content: space-between;
  height: 100%;
}

.hour .description {
  flex-grow: 1;
}

.card-hour {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  border-radius: 5px;
  margin-right: 2rem;
  
}
.card-hour:hover {
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
}
</style>