<template>
  <header class="header">
    <h1>极客 todos</h1>
    <input class="new-todo" autofocus autocomplete="off" placeholder="需要做什么呢 ？" v-model="newTodo" @keyup.enter="addTodo()">
  </header>
</template>

<script>

export default {
  name: 'TheHeader',
  props:{
      todos:Array
  },

  data() {
    return {
      newTodo: '',
    }
  },
  methods: {
    addTodo: function() {
        let value = this.newTodo;

        this.$emit('addTodo',value)
    }
  }
}
</script>