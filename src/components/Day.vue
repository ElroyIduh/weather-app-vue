<template>
  <div>
    <h2>{{ getDate(hour.dt) }}</h2>
    <h2>{{ day.temp.day }}</h2>
    <h2>{{ day.temp.min }}</h2>
    <h2>{{ day.temp.max }}</h2>
    <h2>ICON: {{ day.weather[0].icon }}</h2>
    <img :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`" :alt="day.weather[0].description">
    <hr/>
  </div>
</template>

<script>
export default {
  props: ["day"],
 methods:{
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

</style>