<template>
  <div id="app">
    <h1>Todo application</h1>
    <hr>

    <router-view />
  </div>
</template>

<script>
import todolist from '@/components/todolist'
import addtodo from '@/components/addtodo'
export default {
  name: 'App',
  data() {
    return {
      todos: []
    }
  },
mounted() {
  fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
    .then(json => {
      this.todos = json
    })
  },
  methods: {
    removetodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addtodo(todo) {
      this.todos.push(todo)
    }
  },
  components: {
    todolist, addtodo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
