<template>
  <div id="app">
    <CountryDirectory msg="A Country Directory Project"/>
  </div>
</template>

<script>
import CountryDirectory from './components/CountryDirectory.vue'

export default {
  name: 'App',
  components: {
    CountryDirectory
  }
}
</script>

<style>
body{
    background-image: url('./assets/hero-bg.jpg');
    background-repeat: no-repeat;
    background-attachment: fixed;
    background-size: cover;
    font-family: 'Poppins', sans-serif;
}
</style>
