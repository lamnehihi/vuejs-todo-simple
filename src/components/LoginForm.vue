<template>
  <div class="login-form">
    <h1>Login</h1>
    <input type="text" placeholder="Enter your username" v-model="userInput.name" @keypress.enter="login()">
    <a href="#" rel="noopener noreferrer" @click="$emit('handle-signup-click')">Sign up</a>
  </div>
</template>

<script>
  export default {
    name: 'login-form',
    props: {
      userInput: Object,
      login: Function,
    }
  }
</script>

<style scoped>
a {
  display: block;
  margin-top: .5rem;
  color: inherit;
  text-decoration: none;
}
a:hover {
  text-decoration: underline;
}
</style>