<template>
  <div class="hello">
    <div v-for="stopId in stopsIDs" :key="stopId">
      <stop-table :stop-id="stopId"></stop-table>
      <button class="btn btn-danger" @click="removeStop(stopId)">Usuń</button>
    </div>
  </div>

</template>

<script>
import StopTable from "@/components/StopTable.vue";

export default {
  name: 'HelloWorld',
  components: {StopTable},
  data() {
    return {
      stopsIDs: []
    };
  },
  props: {
    userID: String
  },

  methods: {
    getStops: function () {
      fetch(`http://127.0.0.1:4000/listuserbusstops/${this.userID}`)
          .then(response => response.json())
          .then(data => this.stopsIDs = data.stops);
    },
    removeStop: function (stopId) {
      fetch(`http://127.0.0.1:4000/deletebusstop?busStopId=${stopId}&userId=${this.userID}`, {method: 'DELETE'})
          .then(resp => {
            if (resp.ok) {
              this.getStops();
            }
          });
    }
  },
  mounted() {
    this.emitter.on("stop-added", () => {
      this.getStops();
    });
    this.getStops();
  }

}
</script>>


<style scoped>
h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
