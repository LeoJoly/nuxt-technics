<template>
  <div class="weather">
    <div>
      <h1 class="weather__title">
        The weather !
      </h1>
      <ul v-for="forecastDay in forecastDays" :key="forecastDay.date" class="weather__forecasts">
        <li>
          <div class="weather__forecasts__forecast">
            <h2>{{ forecastDay.date }}</h2>
            <p>Température maximum : {{ forecastDay.day.maxtemp_c }}°C</p>
            <p>Température minimum : {{ forecastDay.day.mintemp_c }}°C</p>
            <p>Chances de pluie : {{ forecastDay.day.daily_chance_of_rain }}%</p>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  async asyncData () {
    const coreForecastDays = await axios.get(
      'https://api.weatherapi.com/v1/forecast.json?key=2d556116f65c4f1da10145144210103&q=paris&days=7&aqi=no&alerts=no'
    ).then(res => res.data.forecast.forecastday)

    // format date
    const forecastDays = coreForecastDays.map((day) => {
      const event = new Date(day.date)

      const options = { weekday: 'long', month: 'long', day: 'numeric' }

      const newDate = event.toLocaleDateString('fr-FR', options)

      return {
        ...day,
        date: newDate
      }
    })

    return { forecastDays }
  }
}
</script>
