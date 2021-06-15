<template>
  <div>
    <h2>{{ day.dt }}</h2>
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
  props: ["day"]
}
</script>

<style>

</style>