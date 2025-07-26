<template>
  <div class="todo">
    <h2>Список задач</h2>

    <form @submit.prevent="addTodo">
      <input v-model="newTodo" placeholder="Новая задача..." />
      <button>Добавить</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        <label>
          <input type="checkbox" v-model="todo.completed" />
          <span :class="{ done: todo.completed }">{{ todo.text }}</span>
        </label>
        <button @click="removeTodo(index)">❌</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTodo: '',
      todos: []
    }
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim()) {
        this.todos.push({
          text: this.newTodo,
          completed: false
        })
        this.newTodo = ''
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1)
    }
  }
}
</script>

<style scoped>
.todo {
  max-width: 400px;
  margin: 0 auto;
}
input[type="text"] {
  width: 70%;
}
.done {
  text-decoration: line-through;
  color: gray;
}
button {
  margin-left: 8px;
}
</style>