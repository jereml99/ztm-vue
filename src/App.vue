<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <login-component></login-component>
  <add-stop user-i-d="6"></add-stop>
  <bus-stops user-i-d="6" />
</template>

<script>
import BusStops from './components/BusStopList.vue'
import AddStop from "@/components/AddStop.vue";
import LoginComponent from "@/components/LoginComponent.vue";

export default {
  name: 'App',
  components: {
    LoginComponent,
    AddStop,
    BusStops: BusStops
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
