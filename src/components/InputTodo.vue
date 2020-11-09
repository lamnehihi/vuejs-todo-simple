<template>
  <div class="todo-input">
    <h3>Hello {{userLogin.name}}</h3>
    <input v-model="todoInput.title" type="text" placeholder="What you gonna do ?" @keypress.enter="addNewTodo()"/>
  </div>
</template>

<script>
  export default {
    name: 'todo-input',
    props: {
      todoInput: Object,
      userLogin: Object,
      addNewTodo: Function,
    }
  }
</script>

<style >

</style>