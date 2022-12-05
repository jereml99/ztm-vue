<template>
  <!--  login form-->
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1>Logowanie</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <form>
          <div class="form-group">
            <label for="login">Login</label>
            <input type="text" class="form-control" id="login" v-model="login" placeholder="Wpisz login">
          </div>
          <div class="form-group">
            <label for="password">Hasło</label>
            <input type="password" class="form-control" id="password" v-model="password" placeholder="Wpisz hasło">
          </div>
          <button type="submit" class="btn btn-primary" @click.prevent="loginUser">Zaloguj</button>
        </form>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "LoginComponent",
  emits: ["user-logged"],
  data() {
    return {
      login: "",
      password: ""
    };
  },
  methods: {
    loginUser: function () {
      fetch(`http://127.0.0.1:4000/login`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify({
          login: this.login,
          password: this.password
        })
      }).then(resp => {
        if (resp.ok) {
         resp.json().then(data => {
           this.$emit("user-logged", data.id);
         });
        } else {
          window.alert("Niepoprawny login lub hasło");
        }
      });
    }
  }
}
</script>

<style scoped>

</style>
