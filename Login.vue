<template>
  <div class="container">
    <form>
      <div class="well">
        <h4>Login Page</h4>

<div> {{message}}</div>
        <div class="form-group">
          <label class="pull-left"> Username </label>
          <input
            type="text"
            class="form-control"
            placeholder="Username"
            v-model="User.username"
            required 
          />
        </div>
        <div class="form-group">
          <label class="pull-left"> Password </label>
          <input
            type="password"
            class="form-control"
            placeholder="Password "
            v-model="User.password"
            required
          />
        </div>
      </div>

      <button
        type="submit"
        class="btn btn-large btn-block btn-success full-width"
        @click="handleSubmit()"
      >
        Submit
      </button>
      <br />
      <button
        type="submit"
        class="btn btn-large btn-block btn-danger full-width"
        @click="handlecancel()"
      >
        Cancel
      </button>
    </form>
  </div>
</template>

<script>
/*eslint-disable */
import axios from "axios";

export default {
  // name: 'login',

  data() {
    return {
      User: {
        // name: "",
        username: "",
        password: "",
        message: "",
      },
      submitted: false,
    };
  },

  methods: {
    handleSubmit() {
      this.submitted = true;
    
      // stop here if form is invalid

      let newUser = {
        // name: this.User.name,
        username: this.User.username,
        password: this.User.password,
        message: ""
      };
      console.log(newUser);
      axios
        .post("http://127.0.0.1:5000/accounts/login", newUser)

        .then((response) => {
          this.message = response;
          console.log(response);
          this.$router.push({ path: "/accounts/login/:username" });
        })
        .catch((error) => {
          console.log(error.response);
        });
    },

    handlecancel() {
      this.submitted = true;
      // stop here if form is invalid

      this.$router.push({ path: "/" });
    },

  }
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
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
