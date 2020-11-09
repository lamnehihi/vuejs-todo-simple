<template>
  <div class="todos">
    <ul>
      <li v-for="todo in todos" :key="todo.id" :class="{done: !todo.status}">
        <span @click="setDone(todo.id)">{{ todo.title }} </span>
        <button @click="deleteOne(todo.id)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "todos",
  props: {
    todos: Array,
    deleteOne: Function,
    setDone: Function,
  },
};
</script>

<style >
.done {
  text-decoration: line-through;
}
</style>