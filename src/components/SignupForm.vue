<template>
  <div class="signup-form">
    <h1>Signup</h1>
    <input type="text" v-model="userSignup.name" @keypress.enter="signup()" placeholder="enter your username">
    <h3>Hello {{userSignup.name}}</h3>
    <a href="#" rel="noopener noreferrer" @click="$emit('handle-login-click')">Ready for sign in?</a>
  </div>
</template>

<script>
  export default {
    name: 'signup-form',
    props: {
      userSignup: Object,
      signup: Function,
    }
  }
</script>

<style>

</style>