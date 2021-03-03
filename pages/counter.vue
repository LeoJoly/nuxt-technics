<template>
  <div class="counter">
    <div>
      <h1 class="counter__title">
        The counter !
      </h1>
      <button class="counter__btn" @click="handleClick()">
        I'm the counter {{ count }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      count: 0
    }
  },
  methods: {
    handleClick () {
      this.count = this.count + 1
    }
  }
}
</script>
