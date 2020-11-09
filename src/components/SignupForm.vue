<template>
  <div class="signup-form">
    <h1>Signup</h1>
    <input type="text" v-model="userSignup.name" @keypress.enter="Signup()">
    <h2>Hello {{userSignup.name}}</h2>
  </div>
</template>

<script>
  export default {
    name: 'signup-form',
    props: {
      userSignup: Object,
      Signup: Function,
    }
  }
</script>

<style>

</style>