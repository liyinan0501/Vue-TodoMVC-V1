<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
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
  },
  computed: {
    isAll: {
      set (checked) {
        this.arr.forEach((obj) => (obj.isDone = checked))
      },
      get () {
        return this.arr.every((item) => item.isDone === true)
      }
    }
  },
  props: ['arr']
}
</script>
