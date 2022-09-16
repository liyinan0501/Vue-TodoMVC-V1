<template>
  <footer class="footer">
    <span class="todo-count"
      ><strong>{{ count }}</strong
      >left</span
    >
    <ul class="filters">
      <li v-for="(item, index) in filterList" :key="index">
        <a
          :class="{ selected: isSelect === item }"
          href="javascript:;"
          @click="changFilter(item)"
          >{{ item }}</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="clearDone">Clear Completes</button>
  </footer>
</template>

<script>
export default {
  props: ['arr'],
  computed: {
    count () {
      return this.arr.length
    }
  },
  data () {
    return {
      filterList: ['all', 'active', 'completed'],
      isSelect: 'all'
    }
  },
  methods: {
    changFilter (item) {
      this.isSelect = item
      this.$emit('filter', item)
    },
    clearDone () {
      this.$emit('clear')
    }
  }
}
</script>
