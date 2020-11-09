<template>
  <div class="input">
    <input v-model="title" type="text" placeholder="" />
  </div>
</template>

<script>
  export default {
    name: 'input',
    props: {
      title: String,
    }
  }
</script>

<style >

</style>