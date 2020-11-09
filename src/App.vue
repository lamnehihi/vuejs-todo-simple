<template>
  <div id="app">
    <Welcome
      v-on:login="isLogin = !isLogin"
      v-on:signup="isSignup = !isSignup"
    />
    <div>
      <LoginForm v-show="isLogin" v-bind:userSignup="userSignup"/>
      <SignupForm
        v-show="isSignup"
        v-bind:userSignup="userSignup"
        v-bind:Signup="Signup"
      />
    </div>
    <h2 v-if="errors.indexOf('This name has already taken !') !== -1">This name has already taken!</h2>
  </div>
</template>

<script>
import Welcome from "./components/Welcome";
import LoginForm from "./components/LoginForm";
import SignupForm from "./components/SignupForm";

export default {
  name: "App",
  components: {
    Welcome,
    LoginForm,
    SignupForm
  },
  data() {
    return {
      isLogin: false,
      isSignup: false,
      userInput: {
        name: "",
      },
      userLogin: {
      },
      userSignup: {
        name: "",
      },
      errors: []
    };
  },
  methods: {
    Login: function () {
      let users = JSON.parse(localStorage.getItem("users"));

      users.forEach((user) => {
        if (
          this.userInput.id === user.id ||
          this.userInput.name === user.name
        ) {
          setTimeout(() => {
            console.log("user " + user.name + "login!");
            this.isLogin = true;
            this.userLogin = user;
            return;
          }, 1000);
        }
      });
    },
    Signup: function () {
      let users = JSON.parse(localStorage.getItem("users"));
      if(!users) {
        users = [];
      }
      this.errors = [];
      users.forEach(user => {
        if(user.name === this.userSignup.name) {
          this.errors.push('This name has already taken !');
          console.log("same name!")
        }
      });
      if(this.errors.indexOf('This name has already taken !') === -1) {
        users.push({ userId: Math.trunc(Math.random() *1000000), name: this.userSignup.name });
        localStorage.setItem("users", JSON.stringify(users));
      }
    },
  }
};
</script>

<style>
#app {
  font-family: Helvetica, sans-serif;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

h1,
h2,
h3,
h4,
h5 {
  font-weight: 200;
}
</style>
