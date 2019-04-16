<template>
  <div id="app" class="todoapp">
    <TodoHead :todos=todos v-on:addTodo="addTodo"></TodoHead>
    <TodoList :todos=todos :filter="filter" :removeTodo="removeTodo"></TodoList>
    <TodoFooter :todos=todos :filter="filter" :removeCompleted="removeCompleted" :changeFilter="changeFilter"></TodoFooter>
  </div>
</template>

<script>
    import '@/assets/base.css'
    import '@/assets/index.css'
    import TodoHead from '@/components/TodoHead.vue'
    import TodoList from '@/components/TodoList.vue'
    import TodoFooter from '@/components/TodoFooter.vue'

export default {
   data(){
    return{
      filter: 'all',
      // beforeEditCache:null,
      // editTodo:null,
      newTodo:'',
      todos:JSON.parse(window.localStorage.getItem('todos_key') || '[]')
    }
  },
  watch:{
    todos:{
      deep:true,
      handler:function(value){
        window.localStorage.setItem('todos_key',JSON.stringify(value))
      }
    }
  },
  methods:{
     changeFilter: function(filter) {
      this.filter = filter
    },
    addTodo: function(value){
      console.log(value)
      // var value = this.newTodo && this.newTodo.trim();
      if (!value) {
        return
      }
      this.todos.push({id: this.todos.length + 1, title:value,completed:false});
      this.newTodo = '';
    },
    removeTodo: function (todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index,1)
    },
    removeCompleted: function () {
      this.todos = this.todos.filter(data => !data.completed);
    },
  },
  components:{
    TodoHead,
    TodoList,
    TodoFooter
  }
}
</script>

<style>
</style>
