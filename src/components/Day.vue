<template>
  <!-- <div> -->
    <!-- <h2>{{ getDate(day.dt) }}</h2>
    <h2>{{ day.temp.day }}</h2>
    <h2>{{ day.temp.min }}</h2>
    <h2>{{ day.temp.max }}</h2>
    <img :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`" :alt="day.weather[0].description">
    <hr/>
  </div> -->

  <div class="card">
  <img :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`" :alt="day.weather[0].description">
  <div class="container">
    <h2>{{ getDate(day.dt) }}</h2>
    <h2>{{ day.temp.day }}</h2>
    <h2>{{ day.temp.min }}</h2>
    <h2>{{ day.temp.max }}</h2>
  </div>
</div>

 <!-- <div class="card">
  <img src="img_avatar.png" alt="Avatar" style="width:100%">
  <div class="container">
    <h4><b>John Doe</b></h4> 
    <p>Architect & Engineer</p> 
  </div>
</div> -->
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

            const formattedDate = + day.substr(-2) + '.' + month.substr(-2) + '.' + year;

            return formattedDate;
        },
 }
}
</script>

<style>
.card {
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
  transition: 0.3s;
  width: 40%;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

.container {
  padding: 2px 16px;
}
</style>