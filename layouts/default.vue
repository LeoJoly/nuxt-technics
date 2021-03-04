<template>
  <div>
    <!-- <nav>
      <ul class="links">
        <li>
          <NuxtLink to="/" class="link">
            Home
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="/counter" class="link">
            Counter
          </NuxtLink>
        </li>
        <li>
          <NuxtLink to="/weather" class="link">
            Weather
          </NuxtLink>
        </li>
      </ul>
    </nav> -->
    <Nuxt />
  </div>
</template>

<style>
html {
  font-family:
    'Inter',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  color: #323232;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

nav {
  background-color: #3b8070;
  height: 72px;
  display: flex;
  justify-content: center;
  align-items: center;
}

ul {
  list-style: none;
}

ul, li {
  margin:0;
  padding: 0;
  text-indent: 0;
  list-style-type: 0;
}

.links {
  width: 50%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

.link {
  color: #fff;
  text-decoration: none;
  font-weight: bold;
}

.link:hover {
  color: #526488;
}

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
}

.title {}

.subtitle {}
</style>
