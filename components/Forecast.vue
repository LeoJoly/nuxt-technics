<template>
  <div class="forecast">
    <div class="forecast__left">
      <div class="forecast__left__icon">
        <img src="//cdn.weatherapi.com/weather/64x64/day/176.png" alt="Weather icon">
      </div>
      <div class="forecast__left__date">
        {{ date }}
      </div>
    </div>
    <div class="forecast__right">
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

<style scoped>
.forecast {
  width: 412px;
  height: 114px;
  padding: 0 1.5rem;
  margin-bottom: 1rem;
  background-color: rgba(255, 255, 255, 0.4);
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: 20px;
  animation: fadein 1s;
}

.forecast__left {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.forecast__left__date {
  width: 30px;
  margin-left: .3rem;
  font-weight: bold;
}

.forecast__right {
  width: 147px;
  height: 46px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.forecast__right__info {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.forecast__right__info__label {
  text-transform: uppercase;
  font-size: .6rem;
}

.forecast__right__info__value {
  color: #8458ff;
  font-weight: bold;
}

@keyframes fadein {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0px);
  }
}
</style>
