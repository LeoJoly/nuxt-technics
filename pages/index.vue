<template>
  <div class="container">
    <div>
      <h1 class="title">
        NUXT Technics
      </h1>
      <p class="subtitle">
        Discovering NUXT.js...
      </p>
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
