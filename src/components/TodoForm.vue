<template>
  <form @submit.prevent="onSubmit">
    <input v-model="input" placeholder="Новая задача..." />
    <button>Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      input: ''
    }
  },
  methods: {
    onSubmit() {
      if (this.input.trim()) {
        this.$emit('add', this.input.trim())
        this.input = ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  gap: 10px;
  margin-bottom: 1rem;
}
input {
  flex: 1;
}
</style>