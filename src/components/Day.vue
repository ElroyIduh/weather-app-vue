<template>


  <div class="card">
  <img :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`" :alt="day.weather[0].description">
  <div class="container">
    <h2>{{ getDay(day.dt) }} - {{ getDate(day.dt) }}</h2>
    <h2>Ø {{ formatTermperature(day.temp.day)  }}</h2>
    <h2>min {{ formatTermperature(day.temp.min) }}</h2>
    <h2>max {{ formatTermperature(day.temp.max) }}</h2>
   
  </div>
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

            const formattedDate =  day.substr(-2) + '.' + month.substr(-2) + '.' + year;

            return formattedDate;
        },
        getDay(dt) {
          const days = ["SO","MO","DI","MI","DO","FR","SA"];

          const date = new Date(dt * 1000)

          const dayNumber = date.getDay()
          return days[dayNumber]
        },
        formatTermperature(temp) {
          const roundedTemp = Math.round(temp)
          return`${roundedTemp} °C`
        }
 }
}
</script>

<style>
.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
  border-radius: 5px;
}
.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}
.container {
  padding: 2px 16px;
  
}
</style>