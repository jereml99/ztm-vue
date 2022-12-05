<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <login-component v-if="!userID" @user-logged="(id) => userID = id"></login-component>
  <add-stop v-if="userID" :user-i-d="userID"></add-stop>
  <bus-stops v-if="userID" :user-i-d="userID" />
  <button v-if="userID" class="btn btn-danger" @click="logout">Wyloguj</button>
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
  },
  data() {
    return {
      userID: ""
    };
  },

  methods: {
    logout: function () {
      this.userID = "";
    }
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
