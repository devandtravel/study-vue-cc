<template>
  <div>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <hr />
    <Loader v-if="loading"/>
    <TodoList v-else-if="todos.length" :todos="todos" @remove-todo="removeTodo" />
    <p v-else>No todos in the list</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
import Loader from '@/components/Loader'
export default {
  name: 'App',
  data() {
    return {
      todos: [],
      loading: true
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => {
        this.todos = json
        this.loading = false
      })
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: { TodoList, AddTodo, Loader }
}
</script>
