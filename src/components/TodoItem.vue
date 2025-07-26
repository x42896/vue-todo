<template>
  <li>
    <label>
      <input type="checkbox" v-model="todo.completed" @change="emitUpdate" />
      <span :class="{ done: todo.completed }">{{ todo.text }}</span>
    </label>
    <button @click="$emit('remove')">❌</button>
  </li>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: Object
  },
  methods: {
    emitUpdate() {
      this.$emit('update')
    }
  }
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
  color: gray;
}
li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 0.5rem;
}
button {
  margin-left: 8px;
}
</style>