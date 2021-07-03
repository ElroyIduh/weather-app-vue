<template>
  <div v-if="hour" class="hour">
    <div>{{ getTime(hour.dt) }}</div>
    <div>
      {{ hour.weather[0].description }}
    </div>
    <div>{{ formatTermperature(hour.temp) }}</div>

    <img
      :src="`http://openweathermap.org/img/wn/${hour.weather[0].icon}@2x.png`"
      :alt="hour.weather[0].description"
    />
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
  width: 30%;
  min-width: 165px;
}

/* .hour {
  width: 30%;
  min-width: 165px;
  overflow-y: auto;
  overflow-x: hidden;
} */
</style>