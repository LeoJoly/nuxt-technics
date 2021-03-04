<template>
  <div class="forecast">
    <div class="forecats__left">
      <div class="forecat__left__icon">
        <img src="//cdn.weatherapi.com/weather/64x64/day/176.png" alt="Weather icon">
      </div>
      <div class="forecast__left__date">
        {{ date }}
      </div>
    </div>
    <div class="forecats__right">
      <div class="forecast__right__info">
        <p class="forecast__right__info__label">
          Min temp
        </p>
        <p class="forecast__right__info__value">
          {{ minTemp }}°C
        </p>
      </div>
      <div class="forecast__right__info">
        <p class="forecast__right__info__label">
          Chance of rain
        </p>
        <p class="forecast__right__info__value">
          {{ rainChance }}%
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Forecast',
  props: ['date', 'minTemp', 'rainChance']
}
</script>
