<template>
  <div>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <hr />
    <TodoList v-if="todos.length" :todos="todos" @remove-todo="removeTodo" />
    <p v-else>No todos in the list</p>
  </div>
</template>

<script>
import TodoList from '@/components/TodoList'
import AddTodo from '@/components/AddTodo'
export default {
  name: 'App',
  data() {
    return {
      todos: []
    }
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => (this.todos = json))
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id)
    },
    addTodo(todo) {
      this.todos.push(todo)
    }
  },
  components: { TodoList, AddTodo }
}
</script>
