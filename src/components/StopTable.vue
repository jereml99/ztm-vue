<template>
  <div class="d-flex">
    <table class="table-bordered" >
      <thead>
      <tr><th colspan="3">{{stopInfo.stopDesc}}</th></tr>
      <tr>
        <th>Linia</th>
        <th>Kierunek</th>
        <th>czas</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="vehicle in vehicles" :key="vehicle.id">
        <td>{{vehicle.line}}</td>
        <td>{{vehicle.heading}}</td>
        <td>{{vehicle.estimatedTime}}</td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>
export default {
  name: "StopTable",
  data() {
    return {
      vehicles: []
    };
  },

  methods: {
    getVehicles: function() {
      fetch(`http://127.0.0.1:4000/stopinfo/${this.stopId}`)
        .then(response => response.json())
        .then(data => {

          data.delay.forEach(vehicle => {
            this.vehicles.push({
              id: vehicle.id,
              line: vehicle.routeId,
              heading: vehicle.headsign,
              estimatedTime: vehicle.estimatedTime
            });
          });
        });
    }
  },

  mounted() {
    this.getVehicles();
  },

  props: {
    stopId: String,
    stopInfo: Object
  },
}
</script>

<style scoped>

</style>
