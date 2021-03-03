<template>
  <div class="container">
    <div>
      <h1 class="title">
        The counter !
      </h1>
      <button @click="handleClick()">
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
