<template>
  <div class="welcome">
    <button v-on:click="$emit('login')">Login</button>
    <button v-on:click="$emit('signup')">Signup</button>
  </div>
</template>

<script>
  export default {
    name: 'welcome',
    props: {
      title: String,
    }
  }
</script>

<style >
  .welcome {
    width: fit-content;
  }
</style>