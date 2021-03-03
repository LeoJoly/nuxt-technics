<template>
  <div class="weather">
    <div>
      <h1 class="weather__title">
        The weather !
      </h1>
      <ul v-for="forecastDay in forecastDays" :key="forecastDay.date" class="weather__forecast">
        <li>
          {{ forecastDay.date }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData () {
    const forecastDays = await axios.get(
      'https://api.weatherapi.com/v1/forecast.json?key=2d556116f65c4f1da10145144210103&q=paris&days=7&aqi=no&alerts=no'
    ).then(res => res.data.forecast.forecastday)

    return { forecastDays }
  }
  // data () {
  //   return {
  //     forecastDays: []
  //   }
  // }
  // methods: {
  //   updateWeather (newForecast) {
  //     this.forecastDays = newForecast
  //   }
  // },
}
</script>
