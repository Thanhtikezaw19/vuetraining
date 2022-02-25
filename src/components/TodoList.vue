<script>
let id = 0

export default {
  data() {
    return {
      newTodo: '',
      hideCompleted: false,
      todos: []
    }
  },
  computed: {
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((t) => !t.done)
        : this.todos
    }
  },
  methods: {
    addTodo() {
      this.todos.push({ id: id++, text: this.newTodo, done: false })
      this.newTodo = ''
    },
    removeTodo(todo) {
      this.todos = this.todos.filter((t) => t !== todo)
    }
  }
}
</script>

<template>
<div class="container">
  <div class="inner">
  <input v-model="newTodo" @keyup.enter="addTodo" />
  <button @click="addTodo">Add Todo</button>
  <ol>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">remove</button>
    </li>
  </ol>
  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
  </div>
  </div>
</template>

<style>
.container {
  width: 50%;
  margin: 0 auto;
  border-radius: 1em;
  border: 1px solid #aa6e6e;
  text-align: left;
  box-shadow: 3px 3px #a19393;
}
.inner {
  margin: 10px;
}
.done {
  text-decoration: line-through;
  color: red;
}
</style>

