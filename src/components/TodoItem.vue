<template>
  <li>
    <span :class="{ done: todo.completed }">
      <input type="checkbox" v-model="todo.completed" />
      <strong>{{ index + 1 }}</strong>
      {{ uppercaseTitle }}
    </span>
    <button class="rm" @click="$emit('remove-todo', todo.id)">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: { type: Object, required: true },
    index: Number
  },
  computed: {
    uppercaseTitle() {
      return this.todo.title.toUpperCase()
    }
  }
}
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
  margin-bottom: 1rem;
}
input {
  margin-right: 1rem;
}

.rm {
  background: red;
  color: white;
  border-radius: 50%;
  font-weight: bold;
}
.done {
  text-decoration: line-through;
}
</style>
