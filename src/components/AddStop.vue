<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Dodaj przystanek</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <form>
          <div class="form-group">
            <label for="stopId">ID przystanku</label>
            <input list="stops" class="form-control" type="search" v-model="resultstopId" placeholder="Wpisz ID przystanku">
            <datalist id="stops">
              <option v-for="stop in stops" :key="stop.stopId" :value="stop.stopId">
                {{stop.stopDesc}}
              </option>
            </datalist>
          </div>
          <button :disabled="!resultstopId" type="submit" class="btn btn-primary" @click.prevent="addStop">Dodaj przystanek</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddStop",
  props: {
    userID: String,
    stops: Array
  },
  emits: ["stop-added"],
  data() {
    return {
      resultstopId: "",
    };
  },

  methods: {
    addStop: function () {
      fetch(`http://127.0.0.1:4000/addbusstop?busStopId=${this.resultstopId}&userId=${this.userID}`, {
        method: "POST"
      }).then(resp => {
        if (resp.ok) {
          this.resultstopId = "";
          this.emitter.emit("stop-added");
        }
      });
    },
  },

}
</script>

<style scoped>

</style>
