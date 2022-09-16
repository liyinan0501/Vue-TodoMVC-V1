<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="Enter"
      autofocus
      v-model="newTodo"
      @keydown.enter="addNew"
    />
  </header>
</template>

<script>
export default {
  data () {
    return {
      newTodo: ''
    }
  },
  methods: {
    addNew () {
      this.$emit('create', this.newTodo)
      this.newTodo = ''
    }
  }
}
</script>
