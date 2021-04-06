<template>
  <div>
    <h2>Todo application</h2>
    <router-link to="/">Home</router-link>
    <hr>
    <addtodo
      @add-todo="addtodo"
    />
    <select v-model="filter">
        <option value="all">All</option>
        <option value="completed">Completed</option>
        <option value="not-completed">Not Completed</option>
    </select>
    <hr>
    <Loader v-if="loading" />
    <todolist
        v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removetodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import todolist from '@/components/todolist'
import addtodo from '@/components/addtodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    }
  },
mounted() {
  fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
    .then(json => {
      setTimeout(()=> {
      this.todos = json
      this.loading = false
      }, 1000)
    })
  },
//   watch: {
//       filter(value) {
//           console.log(value)
//       }
//   },
computed: {
    filteredTodos() {
        if (this.filter === 'all') {
            return this.todos
        }
        if (this.filter === 'completed') {
            return this.todos.filter(t => t.completed)
        }
        if (this.filter === 'not-completed') {
            return this.todos.filter(t => !t.completed)
        }

    }

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
    todolist, addtodo, Loader
  }
}
</script>
