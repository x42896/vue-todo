<template>
  <div class="todo">
    <h2>Список задач</h2>
    <TodoForm @add="addTodo" />
    <ul>
      <TodoItem
        v-for="(todo, index) in todos"
        :key="index"
        :todo="todo"
        @remove="removeTodo(index)"
        @update="saveTodos"
      />
    </ul>
  </div>
</template>

<script>
import TodoForm from './TodoForm.vue'
import TodoItem from './TodoItem.vue'

export default {
  name: 'TodoApp',
  components: {
    TodoForm,
    TodoItem
  },
  data() {
    return {
      todos: []
    }
  },
  mounted() {
    const saved = localStorage.getItem('todos')
    if (saved) {
      this.todos = JSON.parse(saved)
    }
  },
  watch: {
    todos: {
      handler() {
        this.saveTodos()
      },
      deep: true
    }
  },
  methods: {
    addTodo(text) {
      this.todos.push({
        text,
        completed: false
      })
      this.saveTodos()
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
      this.saveTodos()
    },
    saveTodos() {
      localStorage.setItem('todos', JSON.stringify(this.todos))
    }
  }
}
</script>

<style scoped>
.todo {
  max-width: 400px;
  margin: 2rem auto;
}
</style>
