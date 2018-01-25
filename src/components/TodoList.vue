<template>
  <div>
    <p class="tasks">Completed tasks: {{ todos.filter(todo => {return todo.done === true}).length }}</p>
    <p class="tasks">Pending tasks: {{ todos.filter(todo => {return todo.done !== false}).length }}</p>
    <create-todo v-on:create-todo="addTodo"></create-todo>
    <todo v-for="todo in todos" :todo="todo" :key="todo.title" v-on:delete-todo="deleteTodo" v-on:complete-todo="completeTodo"></todo>
  </div>
</template>

<script>
import Todo from './Todo'
import CreateTodo from './CreateTodo'
export default {
  props: ['todos'],
  components: {
    Todo,
    CreateTodo
  },
  methods: {
    deleteTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos.splice(todoIndex, 1)
    },
    addTodo (todo) {
      this.todos.splice(0, 0, todo)
    },
    completeTodo (todo) {
      const todoIndex = this.todos.indexOf(todo)
      this.todos[todoIndex].done = true
    }
  }
}
</script>
