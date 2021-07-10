<template>
   <div class="current">
      <h1>Aktuelles Wetter</h1>
      <p>{{ getDate(current.dt) }}</p>
      <p>{{ current.weather[0].description }}</p>
      <!-- <p>{{ current.weather[0].icon }}</p> -->
      <p>{{ current.temp }}</p>
      <p>{{ current.weather.wind_speed }}</p>
      <!-- <p>{{ quote }}</p> -->
    </div>
</template>

<script>
export default {
  props:["quote", "current"],
   methods:{
    getDate(dt) {
            const date = new Date(dt * 1000);
            
            const month = "0" + (date.getMonth() + 1);
            const day = "0" + date.getDate();
            const year = date.getFullYear();

            const formattedDate = day.substr(-2) + '.' + month.substr(-2) + '.' + year;

            return formattedDate;
        },
   }
}
</script>

<style>

</style>