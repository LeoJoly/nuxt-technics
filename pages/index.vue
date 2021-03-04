<template>
  <div class="container">
    <div class="weatherApp">
      <section class="header">
        <h1 class="header__title">
          Weather forecast
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
              {{ filterValue }}°C
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
              {{ filterValue }}°C
            </p>
          </div>
          <div class="sliders__filter__input">
            <input v-model="filterValue" type="range" min="-10" max="30" step="1">
          </div>
        </div>
      </section>
      <section class="weatherForecast">
        <ul class="weather__forecasts">
          <li v-for="forecastDay in filterData(forecastDays)" :key="forecastDay.date">
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
.container {
  width: 100%;
  min-height: 100vh;
  background: rgb(219,229,255);
  background: linear-gradient(128deg, rgba(219,229,255,1) 0%, rgba(160,126,255,1) 64%, rgba(219,229,255,1) 100%);
  padding-top: 3rem;
}

.weatherApp {
  width: 412px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
}

/* -- Header section -- */
.header {
  margin-bottom: 2rem;
}

.header__title {
  color: #fff;
  font-weight: bold;
  font-size: 2.5rem;
  text-align: center;
}

.header__subtitle {
  text-align: center;
  color: #8458ff;
  font-weight: normal;
  text-transform: uppercase;
  font-size: .9rem;
}

/* -- Header section -- */
.sliders {
  width: 100%;
  margin-bottom: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.sliders__filter {
  width: 43%;
}

.sliders__filter__info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.sliders__filter__info__label {
  color: #fff;
  font-size: .6rem;
  text-transform: uppercase;
}

.sliders__filter__info__value {
  color: #8458ff;
  font-weight: bold;
}

.sliders__filter__input {
  height: 30px;
  margin-top: .3rem;
  padding: 0 1rem;
  background-color: rgba(255, 255, 255, 0.4);
  border-radius: 999px;
  display: flex;
  justify-content: center;
  align-items: center;
}

input[type=range] {
  width: 100%;
  margin: 7px 0;
  background-color: transparent;
  -webkit-appearance: none;
}

input[type=range]:focus {
  outline: none;
}

input[type=range]::-webkit-slider-runnable-track {
  background: #dbe5ff;
  border: 1px solid rgba(1, 1, 1, 0);
  border-radius: 10.7px;
  width: 100%;
  height: 2px;
  cursor: pointer;
}

input[type=range]::-webkit-slider-thumb {
  margin-top: -8px;
  width: 16px;
  height: 16px;
  background: #8458ff;
  border: 1px solid rgba(0, 0, 0, 0);
  border-radius: 50px;
  cursor: pointer;
  -webkit-appearance: none;
}

input[type=range]:focus::-webkit-slider-runnable-track {
  background: #e0e9ff;
}

input[type=range]::-moz-range-track {
  background: #dbe5ff;
  border: 1px solid rgba(1, 1, 1, 0);
  border-radius: 10.7px;
  width: 100%;
  height: 2px;
  cursor: pointer;
}

input[type=range]::-moz-range-thumb {
  width: 16px;
  height: 16px;
  background: #8458ff;
  border: 1px solid rgba(0, 0, 0, 0);
  border-radius: 50px;
  cursor: pointer;
}

input[type=range]::-ms-track {
  background: transparent;
  border-color: transparent;
  border-width: 7px 0;
  color: transparent;
  width: 100%;
  height: 2px;
  cursor: pointer;
}

input[type=range]::-ms-fill-lower {
  background: #d6e1ff;
  border: 1px solid rgba(1, 1, 1, 0);
  border-radius: 21.4px;
}

input[type=range]::-ms-fill-upper {
  background: #dbe5ff;
  border: 1px solid rgba(1, 1, 1, 0);
  border-radius: 21.4px;
}

input[type=range]::-ms-thumb {
  width: 16px;
  height: 16px;
  background: #8458ff;
  border: 1px solid rgba(0, 0, 0, 0);
  border-radius: 50px;
  cursor: pointer;
  margin-top: 0px;
}

input[type=range]:focus::-ms-fill-lower {
  background: #dbe5ff;
}

input[type=range]:focus::-ms-fill-upper {
  background: #e0e9ff;
}
</style>
