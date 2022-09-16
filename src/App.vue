<template>
  <section class="todoapp">
    <TodoHeader @create="createTodo"></TodoHeader>
    <TodoMain :arr="list" @del="delTodo"></TodoMain>
    <TodoFooter :arr="list"></TodoFooter>
  </section>
</template>

<script>
import './styles/base.css'
import './styles/index.css'

import TodoHeader from './components/TodoHeader'
import TodoMain from './components/TodoMain'
import TodoFooter from './components/TodoFooter'

export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter
  },
  data () {
    return {
      list: [
        { id: 100, name: 'LearnReact', isDone: true },
        { id: 201, name: 'LearnVue', isDone: false },
        { id: 103, name: 'LearnTS', isDone: true }
      ]
    }
  },
  methods: {
    createTodo (newTodo) {
      const id =
        this.list.length === 0 ? 100 : this.list[this.list.length - 1].id + 1
      this.list.push({ id, name: newTodo, isDone: false })
    },
    delTodo (id) {
      this.list = this.list.filter((item) => item.id !== id)
    }
  }
}
</script>
