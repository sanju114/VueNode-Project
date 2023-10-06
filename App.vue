<template>
  <header>
    <nav class="navbar">
      <ul class="links-container">
        <li><button @click="toHome">Home</button></li>
        <li><button @click="toLogin">Login</button></li>
        <li><button @click="toSignUp">Sign Up</button></li>
      </ul>
    </nav>
  </header>
  <router-view />
</template>

<script>
export default {
  name: "App",
  methods: {
    toSignUp() {
      this.$router.push({ name: "SignUp" });
    },
    toHome() {
      this.$router.push({ name: "HomeP" });
    },
    toLogin() {
      this.$router.push({ name: "LoginP" });
    }
  }
};
</script>

<style>
.navbar {
  background-color: #ddd;
  padding: 12px 24px;
}

.navbar .links-container {
  display: flex;
  gap: 10px;
  align-items: center;
  justify-content: flex-end;
  margin: 0;
}

li {
  list-style: none;
}

.logo {
  height: 100px;
  margin-left: auto;
  margin-right: auto;
  display: block;
}
.register input,
.login input {
  width: 100%;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-bottom: 30px;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid skyblue;
}
.register input.error,
.login input error {
  border: 1px solid red;
}
.register button,
.login button {
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

.register .error-message,
.login .error-message {
  font-size: 12px;
  color: red;
  position: absolute;
  bottom: 0;
}

.register,
.login {
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
}
</style>
