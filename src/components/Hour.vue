<template>
  <div v-if="hour" class="hour" >
    <div>{{ getDate(hour.dt) }}</div>
    <div>{{ getTime(hour.dt) }}</div>
    <div>
        {{ hour.weather[0].description}}
    </div>
    
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

            const formattedTime = hours + ':' + minutes.substr(-2);

            return formattedTime;
        },
        getDate(dt) {
            const date = new Date(dt * 1000);
            
            const month = "0" + (date.getMonth() + 1);
            const day = "0" + date.getDate();
            const year = date.getFullYear();

            const formattedDate = + day.substr(-2) + ':' + month.substr(-2) + ':' + year;

            return formattedDate;
        },
    }
}
</script>

<style>
.hour {
    display: flex;
    flex-direction: column;
    width: 20%;
}
</style>