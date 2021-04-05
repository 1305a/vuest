<template>
  <div id="app">
    <h1>App</h1>
    <addtodo
      @add-todo="addtodo"
    />
    <hr>
    <todolist
      v-bind:todos="todos"
      @remove-todo="removetodo"
    />
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
