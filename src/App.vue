<template>
  <section class="todoapp">
    <TodoHeader @create="createTodo" :arr="list"></TodoHeader>
    <TodoMain :arr="filteredList" @del="delTodo"></TodoMain>
    <TodoFooter
      :arr="filteredList"
      @filter="filterTodo"
      @clear="clearTodos"
    ></TodoFooter>
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
      list: JSON.parse(localStorage.getItem('VueTodoList')) || [],
      // list: [
      //   { id: 100, name: 'LearnReact', isDone: true },
      //   { id: 201, name: 'LearnVue', isDone: false },
      //   { id: 103, name: 'LearnTS', isDone: true }
      // ],
      getFilter: 'all'
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
    },
    filterTodo (name) {
      this.getFilter = name
    },
    clearTodos () {
      this.list = this.list.filter((item) => item.isDone !== true)
    }
  },
  computed: {
    filteredList () {
      if (this.getFilter === 'active') {
        return this.list.filter((item) => item.isDone === false)
      } else if (this.getFilter === 'completed') {
        return this.list.filter((item) => item.isDone === true)
      } else {
        return this.list
      }
    }
  },
  watch: {
    list: {
      deep: true,
      handler () {
        localStorage.setItem('VueTodoList', JSON.stringify(this.list))
      }
    }
  }
}
</script>
