<template>
   <div class="current">
      <h1>Current</h1>
      <p>{{ current.dt }}</p>
      <p>{{ current.weather[0].description }}</p>
      <p>{{ current.weather[0].icon }}</p>
      <p>{{ current.temp }}</p>
      <p>{{ current.weather.wind_speed }}</p>
      <p>{{ quote }}</p>
    </div>
</template>

<script>
export default {
  props:["quote", "current"]
}
</script>

<style>

</style>