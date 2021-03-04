<template>
  <div class="container">
    <div class="weather__app">
      <section class="header">
        <h1 class="header__title">
          The weather !
        </h1>
        <h2 class="header__subtitle">
          Next 7 days
        </h2>
      </section>
      <section class="sliders">
        <div class="sliders__filter">
          <div class="sliders__filter__info">
            <label for="" class="sliders__filter__info__label">
              min temp
            </label>
            <p class="sliders__filter__info__value">
              {{ filterValue }}
            </p>
          </div>
          <div class="sliders__filter__input">
            <input v-model="filterValue" type="range" min="-10" max="30" step="1">
          </div>
        </div>
        <div class="sliders__filter">
          <div class="sliders__filter__info">
            <label for="" class="sliders__filter__info__label">
              min temp
            </label>
            <p class="sliders__filter__info__value">
              {{ filterValue }}
            </p>
          </div>
          <div class="sliders__filter__input">
            <input v-model="filterValue" type="range" min="-10" max="30" step="1">
          </div>
        </div>
      </section>
      <section class="weatherForecast">
        <ul v-for="forecastDay in filterData(forecastDays)" :key="forecastDay.date" class="weather__forecasts">
          <li>
            <Forecast
              :date="forecastDay.date"
              :minTemp="forecastDay.day.mintemp_c"
              :rainChance="forecastDay.day.daily_chance_of_rain"
            />
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Forecast from '../components/Forecast'

export default {
  components: {
    Forecast
  },
  async asyncData () {
    const coreForecastDays = await axios.get(
      'https://api.weatherapi.com/v1/forecast.json?key=2d556116f65c4f1da10145144210103&q=paris&days=7&aqi=no&alerts=no'
    ).then(res => res.data.forecast.forecastday)

    // format date
    const forecastDays = coreForecastDays.map((day) => {
      const event = new Date(day.date)

      const options = { weekday: 'short', month: 'long', day: 'numeric' }

      const newDate = event.toLocaleDateString('en-US', options)

      return {
        ...day,
        date: newDate
      }
    })

    return { forecastDays }
  },
  data () {
    return {
      filterValue: 0
    }
  },
  methods: {
    filterData (weatherData) {
      return weatherData.filter(data => data.day.mintemp_c >= this.filterValue)
    }
  }
}
</script>

<style scoped>
.filter {
  margin: 1rem 0;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #3b8070;
  font-weight: bold;
}

input {
  margin: 0 .5rem;
}

li {
  margin-bottom: 1rem;
}
</style>
