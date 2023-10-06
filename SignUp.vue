<template>
  <img
    class="logo"
    src="../assets/80690169-man-with-weighing-scale-where-in-expenditure-exceeds-income.jpg"
  />
  <h1 style="text-align: center">Sign Up</h1>

  <div class="register">
    <div class="form-control">
      <input
        type="text"
        v-model="name"
        placeholder="Enter Name"
        :class="{ error: !isNameValid }"
      />
      <p v-if="!isNameValid" class="error-message">
        Name must contain only letters and spaces
      </p>
    </div>

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

    <div class="form-control">
      <input
        type="password"
        v-model="confirmPassword"
        placeholder="Confirm Password"
        :class="{ error: !isConfirmPasswordValid }"
      />
      <p v-if="!isConfirmPasswordValid" class="error-message">
        Passwords do not match
      </p>
    </div>

    <button v-on:click="signUp">Sign Up</button>
    <p>
      <router-link to="/login">Login</router-link>
    </p>
    <p>{{ apiResponse }}</p>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "SignUp",

  data() {
    return {
      name: "",
      email: "",
      password: "",
      confirmPassword: "",
      isNameValid: true,
      isEmailValid: true,
      isPasswordValid: true,
      isConfirmPasswordValid: true,
      apiResponse: ""
    };
  },
  methods: {
    async signUp() {
      this.isNameValid = /^[a-zA-Z\s]+$/.test(this.name);
      this.isEmailValid = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.email);
      this.isPasswordValid = this.password.length >= 6;
      this.isConfirmPasswordValid =
        this.confirmPassword && this.confirmPassword === this.password;

      if (
        this.isNameValid &&
        this.isEmailValid &&
        this.isPasswordValid &&
        this.isConfirmPasswordValid
      ) {
        try {
          let result = await axios.post("http://localhost:3000/SignUp", {
            name: this.name,
            email: this.email,
            password: this.password,
            confirmPassword: this.confirmPassword
          });
          console.warn(result);
          if (result.status === 200) {
            localStorage.setItem("app_user", JSON.stringify(result.data));
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

<style>
/* .logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
  display: block;
}
.register input {
  width: 100%;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.register input.error {
  border: 1px solid red;
}
.register button {
  width: 100%;
  height: 40px;
  border: 1px solid skyblue;
  background: skyblue;
  color: white;
  cursor: pointer;
  margin-left: auto;
  margin-right: auto;
  display: block;
}

.error-message {
  font-size: 12px;
  color: red;
  position: absolute;
  bottom: 0;
}

.register {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 320px;
  margin: 0 auto;
}
.form-control {
  position: relative;
  width: 100%;
}
* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
} */
</style>
