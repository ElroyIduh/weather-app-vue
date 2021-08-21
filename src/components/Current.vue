<template>
   <div class="current">
     
    <img
      :src="`http://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`"
      :alt="current.weather[0].description"/>
      <h2>Aktuelles Wetter in {{ city }}</h2>
      <p>{{ getDate(current.dt) }}</p>
      <p>{{ current.weather[0].description }}</p>
      <p>{{ formatCurrentTermperature(current.temp) }}</p>
      <p>{{ current.weather.wind_speed }}</p>
      
    </div>
</template>

<script>
export default {
  props:["quote", "current", "city"],
   methods:{
    getDate(dt) {
            const date = new Date(dt * 1000);
            
            const month = "0" + (date.getMonth() + 1);
            const day = "0" + date.getDate();
            const year = date.getFullYear();

            const formattedDate = day.substr(-2) + '.' + month.substr(-2) + '.' + year;

            return formattedDate;
        },
        formatCurrentTermperature(temp) {
          const roundedTemp = Math.round(temp)
          return`${roundedTemp} °C`
        },
   }
}
</script>

<style>
 .current {
   padding: 3rem;
 }
</style>