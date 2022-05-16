<template>
  <img class="logo" alt="Vue logo" src="../assets/logo.png" />
  <h1>Sign In</h1>

  <div class="login">
    <input type="text" placeholder="Enter Name" v-model="name" />
    <input type="password" placeholder="Enter Password" v-model="password" />
    <button @click="login">Sign In</button>
    <p>
      <router-link to="/sign-up">Sign Up</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "login-",
  data() {
    return {
      name: "",
      password: "",
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?name=${this.name}&password=${this.password}`
      );
      console.log(result);
      if (result.status == 200 && result.data.length > 0) {
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },

  mounted() {
    let user = localStorage.getItem("user-info");
    if (user) {
      this.$router.push({ name: "Home" });
    }
  },
};
</script>

