<template>
  <table class="table-responsive-lg">
    <thead>
      <tr>
        <th>Linia</th>
        <th>Kierunek</th>>
        <th>Szacowany czas przyjazdu</th>
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
    stopId: Number
  },
}
</script>

<style scoped>

</style>
