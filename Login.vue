<template>
  <img
    class="logo"
    src="../assets/80690169-man-with-weighing-scale-where-in-expenditure-exceeds-income.jpg"
  />
  <h1 style="text-align: center">Login</h1>

  <div class="login">
    <div class="form-control">
      <input
        type="text"
        v-model="email"
        placeholder="Enter Email"
        :class="{
          error: !isEmailValid
        }"
      />
      <p v-if="!isEmailValid" class="error-message">Invalid email format</p>
    </div>
    <div class="form-control">
      <input
        type="password"
        v-model="password"
        placeholder="Enter Password"
        :class="{ error: !isPasswordValid }"
      />
      <p v-if="!isPasswordValid" class="error-message">
        Password must be at least 6 characters long
      </p>
    </div>

    <button v-on:click="login">Login</button>
    <p>
      <router-link to="/sign-up">Sign Up</router-link>
    </p>
  </div>
</template>
<script>
import axios from "axios";

export default {
  name: "LoginP",

  data() {
    return {
      email: "",
      password: "",
      isEmailValid: true,
      isPasswordValid: true
    };
  },
  methods: {
    async login() {
      this.isEmailValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.email);
      this.isPasswordValid = this.password.length >= 6;
      if (this.isEmailValid && this.isPasswordValid) {
        try {
          let result = await axios.post("http://localhost:3000/login", {
            email: this.email,
            password: this.password
          });
          console.warn(result);
          if (result.status === 200) {
            //localStorage.setItem("app_user", JSON.stringify(result.data));
          }
        } catch (error) {
          console.log(error);
          this.apiResponse = error.response.data.message;
        }
      }
    }
  }
};
</script>
